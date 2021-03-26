# CSS Isolation Bug Demonstration

This repo demonstrates a problem with CSS Isolation in Blazor when the solution includes CSS files that are dynamically created.

Normally, if a component with a .razor extension and css file with a .razor.css extension are in the same directory, Blazor will generate a bundle that includes this .razor.css file. However, if that css file is updated during the pre-build process, the Blazor bundle still references the old contents of the file (and will omit it entirely if that file didn't exist before).

This is simulated by copying a file from the wwwroot/css folder to Shared/NavMenu.razor.css in a pre-build target. In practice, it is also likely to happen if you are using a CSS preprocessor like Sass and have a build-time process for compiling your .razor.scss files to .razor.css.

## Running the demo

Start the project by running `dotnet run`. The problem will become apparent because the sidebar menu will not be visible. If you stop the server and restart it, the problem goes away because the css files now exist to be included in the bundle.
