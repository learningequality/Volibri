# Volibri
Version Control for Kolibri UI/UX design


**The problems:**

It appears to us that a version control solution is needed to accommodate the collaborative design work we've done for Kolibri.
There are 3 major issues we want to address with this version control solution:

1. Be able to easily trace back the design decision making history. Following describes a typical issue we are facing more and more often. After many iterations for an UI element, it becomes unclear to us how we arrived at the current approach, and start bringing arguments up that later we realized were fully discussed before.

2. Be able to keep design modifications in sync across the team. Our design team has collectively experienced this pain that if one of us updates the design of a shared UI element, all of us have to find the files that uses this shared element and manually update it.

3. Be able to asynchronously comment on and reply to new designs. We used to post designs in our online chat room to get feedbacks. But just like design takes inspiration, criticizing design also takes inspiration. Since we cannot guarantee to get inspired in time, let's do it asynchronously via Pull Request.

**The solution:**

Terminology: `link-import` means using `Place-Linked-Bitmap` plugin's `Place Bitmap as New Layer` method to create a linkage of the external image file. Therefore, whenever the external image files changed, we can use the `Update All Bitmaps` method to update all link-imported images in the Sketch file.

Issue 1 and 3 stated above are addressed by managing the project on github. 
For issue 2, we rely on the Sketch plugin `Place-Linked-Bitmap` to create external linkage between a external image file and mulitple Sketch mockup files. If the external image file gets modified, all Sketch mockup files that `link-import` the image file will get updated automatically. The external image file can also be created by Sketch. Using the `sketch-image-compressor` plugin, we can export Sketch Slices at once to lossless compressed PNG files.
There is an example how to build a list UI element uisng this approach.

1. We create 2 Sketch files, `container_element.sketch` and `list_item_element.sketch`.

2. We use the `Make Exportable` feature of Sketch to generate 2 image files, `container.png` and `list-item.png`. (Note: because we installed `sketch-image-compressor` plugin, all exported images will be automatically losslessly compressed.)

3. We create another Sketch file `list.sketch` that `link-import` the `container.png` and `list-item.png`, place the imported list-item inside the imported container, copy paste(the duplications will keep the linkage to the external image) the list-item couple times to make it looks like a proper list UI element.

Say later you want to change the background color of the list-item, you can open the `list_item_element.sketch` and change the background color. Export image again to update the `list-item.png` with your modification. (it is important to keep the image file name unchanged!). Open your `list.sketch`, click `Plugins/Place Linked Bitmap/Update All Bitmap`, you will see that all the list-items' background color get changed to the new color.
It gets more interesting when you apply this pattern recursively. Go ahead and select all elements that consists the list inside `list.sketch` and create a `Symbol` called `list`. Export this symbol you get `list.png`. Now you can `link-import` this `list.png` in other Sketch mockup files, such as your `Learn_page.sketch` and `Explore_page.sketch`, and they will get auto updated if you changed anything in `list.png`.

**The dependencies:**

You need to install the following plugins.

1. [Place-Linked-Bitmap](https://github.com/frankko/Place-Linked-Bitmap) (a Sketch plugin that enables `link-import` images).

2. [sketch-image-compressor](https://github.com/BohemianCoding/sketch-image-compressor) (a Sketch plugin that exports all your slices to lossless compressed pngs).

**Let's get started:**

1. `fork` this Repo.

2. `git clone` your forking repo.

3. Create some PNG formatted UI elements using Sketch and `link-import` them in other Sketch file to create more complicated UI elements.

4. Commit both your source file(the Sketch files) and your image files(the Exported PNG files), so that other people can `link-import` your images in their mockup. Future modifications can be done by editing your source files and re-export the image files.

5. Open a PR with proper descriptions stating the design consideration(a PR template will be added soon).

6. Everyone can give feedbacks by commenting your PR.

7. After all concerns addressed, another designer with merge privilege can merge your PR to make your new design offically available to everyone in the company. :shipit:

Notice: If you like to try a couple different desgins, you should create branches fro each design.
