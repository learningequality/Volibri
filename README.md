# Volibri
Version Control for Kolibri UI/UX design


**The problems:**

It appears to us that a version control solution is needed to accommodate the collaborative design work we've done for Kolibri.
There are 3 major issues we want to address with this version control solution:

1. Be able to easily trace back the design decision making history. Following describes a typical issue we are facing more and more often. After many iterations for an UI element, it becomes unclear to us how we arrived at the current approach, and start bringing arguments up that later we realized were fully discussed before.

2. Be able to keep design modifications in sync across the team. Our design team has collectively experienced this pain that if one of us updates the design of a shared UI element, all of us have to find the files that uses this shared element and manually update it.

3. Be able to asynchronously comment on and reply to new designs. We used to post designs in our online chat room to get feedbacks. But just like design takes inspiration, criticizing design also takes inspiration. Since we cannot guarantee to get inspired in time, let's do it asynchronously via Pull Request.

**The solution:**

Issue 1 and 3 stated above are addressed by managing the project on github. 
For issue 2, we rely on the Sketch plugin `Place-Linked-Bitmap` to create external linkage between a external image file and mulitple Sketch mockup files. If the external image file gets modified, all Sketch mockup files that `link-import` the image file will get updated automatically. Because Sketch supports `export as image file`, we can create the external image file using Sketch.
There is an example how to build a list UI element uisng this approach.

1. We create 2 Sketch files, `container_element.sketch` and `list_item_element.sketch`.

2. We use the `export as image file` feature of Sketch to generate 2 image files, `container.png` and `list-item.png`.

3. We create another Sketch file `list.sketch` that `link-import` the `container.png` and `list-item.png`, place the imported list-item inside the imported container, copy paste the imported list-item couple times to make it looks like a proper list UI element.

Now you are done with the creation part. Let's get into the more exiting modification part. Say you want to change the background color of the list-item, you can open the `list_item_element.sketch` to change the background color. After you finished the modification, export image again. You will replace the `list-item.png` with your newer version. (it is important to keep the image file name unchanged!). Open your `list.sketch`, click `Plugins/Place Linked Bitmap/Update All Bitmap`, you will see that all the list-items' background color get changed to the new color.
Even more exciting, you can export an image from `list.sketch`, let's call it `list.png`, and you can `link-import` this `list.png` in other Sketch mockup files, such as your `Learn_page.sketch` and `Explore_page.sketch`, and they will get auto updated if you changed anything in `list.png`.

**The dependencies for this solution:**

1. [Sketch](https://www.sketchapp.com/) (necessary to create the assembled mockup that `link-imports` UI element images).

2. [Place-Linked-Bitmap](https://github.com/frankko/Place-Linked-Bitmap) (a Sketch plugin that enables `link-import` images).

**Typical workflow:**

1. fork this Repo.

2. git clone your forking repo.

3. find the source file you like to modify(or create a source file if you are introducing new elements), make your modifications, when you finished, generate images(PNG, JPG, PSD...) from the source file.

4. commit both the source file and the image files, so that the mockup can `link-import` your images and additional modifications can be done by editing the source file.

5. open a PR with proper descriptions.

6. another designer with merge privilege can merge your PR to make your new design offically available to everyone in the company. :shipit:

Notice: If you like to try a couple different desgins, you should create branches fro each design.
