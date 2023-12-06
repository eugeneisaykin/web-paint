The Paint Graphic Editor
This graphics editor application is developed using the Svelte framework. The design is minimalistic, inspired by the old Paint from Windows XP to ensure ease of use.

Installation and Launch
First, make sure that you have Node installed.js on your computer.

Clone the repository:

bash
Copy code
git clone https://github.com/your_username/paint-app.git
Go to the project directory:

bash
Copy code
cd paint-app
Install dependencies:

bash
Copy code
npm install
Launch the application:

bash
Copy code
npm start
The application will be available at http://localhost:3000 .

Main functions
Canvas for drawing: The main place for creativity.

Straight Line: Draws a straight line with the selected thickness.

Pencil: Allows you to draw freely on a canvas with a selected thickness.

Rectangle: Draws a rectangle with the specified frame thickness, frame color, and fill.

Triangle: Draws a triangle with the selected border thickness, border color, and fill.

Circle: Draws a circle with the selected frame thickness, frame color, and fill.

Color selection: Fields for selecting the main and auxiliary colors (frame and fill).

Predefined colors: PCM is the main color, LCM is the auxiliary color.

Eraser: Removes the drawn elements.

Image Saving: Saves the current image.

Warning before closing: Warning that changes are not saved when trying to close the window.

Resizing the canvas: Allows the user to resize the canvas.

Tape measure on canvas: An auxiliary ruler for measuring distances.

Cleaning the entire sheet: Removes all elements from the canvas.

Launch the app and start drawing on the canvas.

Select a tool or color from the corresponding panels.

Use the context menu to quickly select colors.

Save your work using the "Save Image" option.

Before closing the window, the application will warn you about unsaved changes.

Remarks
Browser support: It is recommended to use modern browsers (Chrome, Firefox, Safari) for better performance.

Thank you for using our Paint graphic editor! 🎨