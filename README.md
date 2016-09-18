# Volibri
Version Control for Kolibri UI/UX design


**The problems:**

It appears to us that a version control solution is needed to accommodate the collaborative design work we've done for Kolibri.
There are 3 major issues we want to address with this version control solution:

1. Be able to easily trace back the design decision making history. The following describes a typical issue we are facing more and more often. After many iterations for an UI element, it becomes unclear to us how we arrived at the current approach, and start bringing arguments up that later we realized were fully discussed before.

2. Be able to keep design modifications in sync across the team. Our design team has collectively experienced this pain that if one of us updates the design of a shared UI element, there is no efficient way for her to inform everyone in the team(devs and other designers) about the modification. Afterwards all of us have to find the files that use this shared element and manually update it.

3. Be able to asynchronously comment on and reply to new designs. We currently post designs in our online chat room to receive feedback. This can be an issue if comments were unseen and pushed up in the chatroom. It can be very inconvenient and difficult to access the feedback again. It makes a lot sense to asynchronously comment and reply via Pull Request.

**The solution:**

Issue 1 and 3 stated above are addressed by managing the project on github. 

For issue 2, we want to have a single source of truth -- `the master repo` that is always up to date. So you can always work on the latest design version. We also want that multiple designers can checkout the same file from the master reop and work on it at the same time, later merge everyone's works in the same file via Pull Requests. To achieve the above stated, we need a mergable image format. It is impossible to merge binary files such as bitmap images(PNG, JPG) and `.sketch` format, PSD). Therefore, we decided to use the text based format SVG.

Fortunately, our most widely used design tool Sketch has awesome SVG support and has a plugin system that allows us to customize our workflow.

Because Sketch will add some additional code to the SVG files when save or export or open via the built-in file operations, merge conflicts are likely introduced. To make our SVG easier to merge, we rely on the Sketch plugin [Sketch-Linked-SVG](https://github.com/66eli77/Sketch-Linked-SVG) for all file operations, including open, save, import, export, and update SVG files. The goal is to keep the SVG code as concise and consistent as possible.  

There is a short description about what the plugin's file operations do:

- `Update Linked SVGs` -- reload all SVG layers marked with `@@`

- `Import Linked SVG` -- import external SVG file into a SVG layer and mark the layer with `@@` follow by the relative location of the external SVG file.

- `Export SVG` -- save the selected layers into a SVG file.

- `Open SVG` -- open external SVG file in a `page`.

- `Save SVG` -- save all layers in the current `page` into a SVG file.

**Let's get started:**

1. `fork` this Repo.

2. `git clone` your forking repo.

3. Install the plugin.

4. For creating new design, use Sketch as you normally would.

5. For modifing existing design, load the SVG using the plugin's `Open SVG` method, and you will be able to work on it as usual sketch file.

6. For adding external SVG(normally Kolibri's default elements) to your design, use the plugin's `Import Linked SVG`. If these external SVGs changed in the future, you can use the plugin's `Update Linked SVGs` to update them.

7. To save your work, use the plugin's `Export SVG` or `Save SVG` method.

8. Commit only your SVG files.

9. Open a PR with proper descriptions stating the design consideration.

10. Everyone can now give feedbacks by commenting your PR, and you can reply on the same PR.

11. After all concerns addressed, another designer with merge privilege can merge your PR into master to make it available to everyone in the team. :shipit:

Notice: If you like to try a couple different design, you should create branches for each design.

**The dependencies:**

You need to install the following plugins.

1. [Sketch-Linked-SVG](https://github.com/66eli77/Sketch-Linked-SVG)

2. [sketch-palettes](https://github.com/andrewfiorillo/sketch-palettes) (Let you load `kolibri_color_palette.sketchpalette` into sketch).
