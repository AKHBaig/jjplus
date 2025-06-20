TITLE: Element Palette (Stencil) in JointJS
DESCRIPTION: This documentation describes the JointJS+ Element Palette plugin, also known as Stencil. It provides a draggable palette of JointJS Elements that users can drag and drop onto a JointJS Paper. The example code demonstrates how to install and initialize the Stencil plugin, associating it with a JointJS Paper instance.
SOURCE: [https://docs.jointjs.com/learn/features/element-palette](https://docs.jointjs.com/learn/features/element-palette)

LANGUAGE: Javascript
CODE:

```javascript
import { dia, shapes, ui } from '@joint/plus';

const graph = new dia.Graph({}, { cellNamespace: shapes });
const paper = new dia.Paper({
 el: document.getElementById('paper'),
 width: 500,
 height: 300,
 model: graph,
 cellViewNamespace: shapes
});
const stencil = new ui.Stencil({
 paper,
 width: 200,
 height: 300
});

document.getElementById('stencil-holder').appendChild(stencil.render().el);
```

Here is the documentation in the requested format for each URL:

-----

TITLE: Property Editor and Viewer (Inspector) in JointJS
DESCRIPTION: The Inspector plugin in JointJS+ enables the creation of an editor and viewer for Cell model properties. It provides a two-way data binding between the Cell model and a dynamically generated HTML form, allowing for declarative definition of input fields. This flexibility allows configuring both visual attributes and custom data on the Cell model, making it a versatile component for applications.
SOURCE: [https://docs.jointjs.com/learn/features/property-editor-and-viewer](https://docs.jointjs.com/learn/features/property-editor-and-viewer)

LANGUAGE: Javascript
CODE:

```javascript
import { ui } from '@joint/plus';

const inspector = new ui.Inspector(options);

document.getElementById('inspector-holder').appendChild(inspector.render().el);
```

-----

TITLE: Toolbar in JointJS
DESCRIPTION: The JointJS+ Toolbar plugin enhances applications by providing various tools, allowing integration of built-in controls for managing other JointJS+ plugins (like zoom for PaperScroller, undo/redo for CommandManager) or custom functionalities. The toolbar serves as a container for these tools, which are referred to as "Widgets."
SOURCE: [https://docs.jointjs.com/learn/features/toolbar](https://docs.jointjs.com/learn/features/toolbar)

LANGUAGE: Javascript
CODE:

```javascript
import { ui } from '@joint/plus';
const toolbar = new ui.Toolbar({
tools: [
{ type: 'checkbox' },
{ type: 'range', name: 'slider', min: 0, max: 10, step: 1 },
{ type: 'separator' },
{ type: 'toggle', name: 'toggle', label: ''},
'separator', // also possible, use defaults
{ type: 'inputText' },
{ type: 'button', name: 'ok', text: 'Ok' },
{ type: 'button', name: 'cancel', text: 'Cancel' },
{ type: 'separator' }
]
});
document.getElementById('toolbar-holder').appendChild(toolbar.render().el);
```

-----

TITLE: Zoom & Scroll (PaperScroller) in JointJS
DESCRIPTION: The JointJS+ PaperScroller plugin provides functionalities for scrolling, panning, zooming, centering, and auto-resizing the content of a JointJS Paper. It acts as a wrapper around the Paper element, enabling enhanced navigation and display of diagrams.
SOURCE: [https://docs.jointjs.com/learn/features/zoom-and-scroll](https://docs.jointjs.com/learn/features/zoom-and-scroll)

LANGUAGE: Javascript
CODE:

```javascript
import { dia, shapes, ui } from '@joint/plus';

const graph = new dia.Graph({}, { cellNamespace: shapes });
const paper = new dia.Paper({ width: 2000, height: 2000, model: graph, cellViewNamespace: shapes });
const paperScroller = new ui.PaperScroller({ paper: paper });
document.getElementById('paper').appendChild(paperScroller.render().el);
```

-----

TITLE: Minimap (Navigator) in JointJS
DESCRIPTION: The JointJS+ Navigator plugin implements a minimap feature, displaying a smaller overview of a larger diagram. It allows users to quickly navigate complex diagrams using a pannable and resizable rectangle within the minimap view.
SOURCE: [https://docs.jointjs.com/learn/features/minimap](https://docs.jointjs.com/learn/features/minimap)

LANGUAGE: Javascript
CODE:

```javascript
import { ui } from '@joint/plus';
const nav = new ui.Navigator({
paperScroller,
width: 300,
height: 200,
padding: 10,
zoomOptions: { max: 2, min: 0.2 }
});
```

-----

TITLE: Halo in JointJS
DESCRIPTION: The JointJS+ Halo plugin provides a control panel that appears above an element, offering various tools for user interaction. It gives users immediate control over their elements through an easily accessible set of actions. The `ui.Halo` requires the view of a cell to display the halo.
SOURCE: [https://docs.jointjs.com/learn/features/halo](https://docs.jointjs.com/learn/features/halo)

LANGUAGE: Javascript
CODE:

```javascript
import { dia, shapes, ui } from '@joint/plus';
const graph = new dia.Graph({}, { cellNamespace: shapes });
const paper = new dia.Paper({
 el: document.getElementById('paper'),
 width: 500,
 height: 500,
 model: graph,
 cellViewNamespace: shapes
});
paper.on('element:pointerup', (elementView) => {
 const halo = new ui.Halo({
 cellView: elementView,
 type: 'overlay'
 });
 halo.render();
});
```

-----

TITLE: Selection in JointJS
DESCRIPTION: The JointJS+ Selection plugin enables the ability to select elements on the paper. It facilitates element selection, allows moving the entire selection in one go, and supports manipulating the selection by selecting or deselecting individual elements.
SOURCE: [https://docs.jointjs.com/learn/features/selection](https://docs.jointjs.com/learn/features/selection)

LANGUAGE: Javascript
CODE:

```javascript
import { ui } from '@joint/plus';
const selection = new ui.Selection({
paper: paper,
// optional, a custom collection that inherits from mvc.Collection
collection: new MyCollection
});
```

-----

TITLE: Selection Region in JointJS
DESCRIPTION: The JointJS+ Selection Region feature allows users to select areas of various shapes and sizes on a diagram. It provides built-in selection regions like RectangularSelectionRegion, PolygonalSelectionRegion, and RangeSelectionRegion, enabling functionalities such as selecting elements, zooming into areas, or creating custom selection regions.
SOURCE: [https://docs.jointjs.com/learn/features/selection-region](https://docs.jointjs.com/learn/features/selection-region)

LANGUAGE: Javascript
CODE:

```javascript
const region = new ui.RectangularSelectionRegion({ paper });
paper.on('blank:pointerdown', async () => {
const area = await region.getUserSelectionAsync();
if (!area) return;
const elements = graph.findModelsInArea(area);
/* do something with the elements */
});
```

-----

TITLE: Resize & Rotate (FreeTransform) in JointJS
DESCRIPTION: The JointJS+ FreeTransform plugin enables the creation of a control panel above an element, allowing users to resize an element in any direction and rotate it. This provides interactive manipulation capabilities for diagram elements.
SOURCE: [https://docs.jointjs.com/learn/features/resize-and-rotate](https://docs.jointjs.com/learn/features/resize-and-rotate)

LANGUAGE: Javascript
CODE:

```javascript
import { dia, shapes, ui } from '@joint/plus';
const graph = new dia.Graph({}, { cellNamespace: shapes });
const paper = new dia.Paper({
el: document.getElementById('paper'),
width: 500,
height: 500,
model: graph,
cellViewNamespace: shapes
});
paper.on('element:pointerup', (elementView) => {
const freeTransform = new ui.FreeTransform({ cellView: elementView });
freeTransform.render();
});
```

-----

TITLE: Undo & Redo (CommandManager) in JointJS
DESCRIPTION: The JointJS+ CommandManager plugin tracks graph changes, enabling users to navigate the history of modifications by performing undo and redo operations. It listens to graph changes, stores the delta of each change as a command, and maintains separate stacks for undo and redo operations.
SOURCE: [https://docs.jointjs.com/learn/features/undo-redo](https://docs.jointjs.com/learn/features/undo-redo)

LANGUAGE: Javascript
CODE:

```javascript
import { dia, shapes } from '@joint/plus';
const graph = new dia.Graph({}, { cellNamespace: shapes });
const commandManager = new dia.CommandManager({ graph });
```

-----

TITLE: Copy & Paste (Clipboard) in JointJS
DESCRIPTION: The JointJS+ Clipboard plugin provides functionality for copying and pasting cells within and between diagrams. It optionally supports storing cells in HTML5 localStorage, allowing copy-paste operations to persist across browser sessions or refreshes. The clipboard can also facilitate copying cells from one paper and pasting them to another.
SOURCE: [https://docs.jointjs.com/learn/features/copy-and-paste](https://docs.jointjs.com/learn/features/copy-and-paste)

LANGUAGE: Javascript
CODE:

```javascript
import { ui } from '@joint/plus';
const clipboard = new ui.Clipboard({ useLocalStorage: false });
```
-----

TITLE: Keyboard Shortcuts in JointJS
DESCRIPTION: The JointJS+ Keyboard plugin allows you to implement custom keyboard shortcuts in your application. It provides a flexible way to define and handle keyboard events, enabling a more efficient user experience for diagram manipulation.
SOURCE: [https://docs.jointjs.com/learn/features/keyboard-shortcuts](https://docs.jointjs.com/learn/features/keyboard-shortcuts)

LANGUAGE: Javascript
CODE:

```javascript
import { ui } from '@joint/plus';

const keyboard = new ui.Keyboard();

keyboard.on('ctrl+c', () => console.log('ctrl+c pressed'));
keyboard.on('ctrl+v', () => console.log('ctrl+v pressed'));
keyboard.on('del', () => console.log('del pressed'));
```

-----

TITLE: Inline Text Editing in JointJS
DESCRIPTION: JointJS+ offers a powerful Inline Text Editing feature that provides a rich-text editor directly on any SVG text element. This allows users to easily modify text content within their diagrams without needing external input fields.
SOURCE: [https://docs.jointjs.com/learn/features/inline-text-editing](https://docs.jointjs.com/learn/features/inline-text-editing)

LANGUAGE: Javascript
CODE:

```javascript
import { ui } from '@joint/plus';

const inlineTextEditor = new ui.InlineTextEditor({
    text: 'Double click to edit',
    width: 200,
    height: 30
});

document.getElementById('editor-holder').appendChild(inlineTextEditor.render().el);
```

-----

TITLE: Validations in JointJS
DESCRIPTION: JointJS+ provides validation capabilities to ensure the integrity and correctness of your diagrams. This feature allows you to define rules and checks that govern the placement, connection, and data of elements, helping to maintain a consistent and valid diagram structure.
SOURCE: [https://docs.jointjs.com/learn/features/validations/](https://docs.jointjs.com/learn/features/validations/)

LANGUAGE: Javascript
CODE:

```javascript
import { dia, linkTools, shapes, util } from '@joint/plus';

const graph = new dia.Graph({}, { cellNamespace: shapes });
const paper = new dia.Paper({
    el: document.getElementById('paper'),
    model: graph,
    width: 800,
    height: 600,
    gridSize: 10,
    drawGrid: true,
    background: {
        color: '#f8f8f8'
    },
    defaultLink: new shapes.standard.Link(),
    validateConnection: function(cellViewS, magnetS, cellViewT, magnetT, end, linkView) {
        // Only allow a connection from an output port to an input port
        return magnetS.getAttribute('port-group') === 'out' && magnetT.getAttribute('port-group') === 'in';
    },
    cellViewNamespace: shapes
});
```

-----

TITLE: Data Validity in JointJS Validations
DESCRIPTION: The Data Validity feature within JointJS+ validations allows you to define rules for the internal data of your cells. This ensures that the data stored within elements conforms to specified constraints, enhancing the overall consistency and reliability of your diagram's underlying data model.
SOURCE: [https://docs.jointjs.com/learn/features/validations/data-validity](https://docs.jointjs.com/learn/features/validations/data-validity)

LANGUAGE: Javascript
CODE:

```javascript
import { dia, shapes, util } from '@joint/plus';

const graph = new dia.Graph({}, { cellNamespace: shapes });

const myElement = new shapes.standard.Rectangle({
    position: { x: 50, y: 50 },
    size: { width: 100, height: 40 },
    attrs: {
        label: { text: 'My Element' }
    }
});
graph.addCell(myElement);

// Example of defining data validation for 'value' property
myElement.set('isValidValue', true, { silent: true }); // Initial state

myElement.on('change:value', (cell, newValue) => {
    const isValid = newValue > 0; // Simple validation: value must be positive
    cell.set('isValidValue', isValid);
    cell.attr('body/stroke', isValid ? 'green' : 'red');
});

// Try changing the value to see validation in action
myElement.set('value', 10); // Valid
myElement.set('value', -5); // Invalid (stroke turns red)
```

-----

TITLE: Shortest Path Algorithm in JointJS
DESCRIPTION: JointJS+ includes algorithms for graph analysis, such as the Shortest Path algorithm. This feature helps in finding the most efficient path between two nodes (elements) in a graph, which is useful for routing, network analysis, and other diagram-based optimizations.
SOURCE: [https://docs.jointjs.com/learn/features/algorithms/shortest-path](https://docs.jointjs.com/learn/features/algorithms/shortest-path)

LANGUAGE: Javascript
CODE:

```javascript
import { dia, g, shapes } from '@joint/plus';

const graph = new dia.Graph({}, { cellNamespace: shapes });

// Create some elements and links to form a graph
const r1 = new shapes.standard.Rectangle({ position: { x: 50, y: 50 }, size: { width: 50, height: 30 } });
const r2 = new shapes.standard.Rectangle({ position: { x: 150, y: 50 }, size: { width: 50, height: 30 } });
const r3 = new shapes.standard.Rectangle({ position: { x: 100, y: 150 }, size: { width: 50, height: 30 } });
const link1 = new shapes.standard.Link({ source: { id: r1.id }, target: { id: r2.id } });
const link2 = new shapes.standard.Link({ source: { id: r2.id }, target: { id: r3.id } });
const link3 = new shapes.standard.Link({ source: { id: r1.id }, target: { id: r3.id } });

graph.addCells([r1, r2, r3, link1, link2, link3]);

// Find the shortest path from r1 to r3
const path = graph.shortestPath(r1, r3);

if (path) {
    console.log('Shortest path:', path.map(cell => cell.id));
} else {
    console.log('No path found.');
}
```

-----

TITLE: Snaplines for Elements in JointJS
DESCRIPTION: The JointJS+ Snaplines feature provides visual alignment guides when moving elements on the paper. These snaplines help users precisely position and align elements relative to each other, ensuring a clean and organized diagram layout.
SOURCE: [https://docs.jointjs.com/learn/features/snap-to-objects/snaplines-for-elements](https://docs.jointjs.com/learn/features/snap-to-objects/snaplines-for-elements)

LANGUAGE: Javascript
CODE:

```javascript
import { dia, ui, shapes } from '@joint/plus';

const graph = new dia.Graph({}, { cellNamespace: shapes });
const paper = new dia.Paper({
    el: document.getElementById('paper'),
    model: graph,
    width: 800,
    height: 600,
    gridSize: 10,
    drawGrid: true,
    background: { color: '#f8f8f8' },
    snapLinks: true,
    linkPinning: false,
    cellViewNamespace: shapes
});

const snaplines = new ui.Snaplines({ paper: paper });

paper.on({
    'element:pointerdown': (elementView) => {
        snaplines.start(elementView);
    },
    'element:pointerup': (elementView) => {
        snaplines.stop();
    }
});

const r1 = new shapes.standard.Rectangle({ position: { x: 50, y: 50 }, size: { width: 100, height: 50 } });
const r2 = new shapes.standard.Rectangle({ position: { x: 200, y: 100 }, size: { width: 100, height: 50 } });
graph.addCells([r1, r2]);
```

-----

TITLE: Stack Layout View (Drag & Drop) in JointJS
DESCRIPTION: The JointJS+ Stack Layout View is a specialized component for drag and drop interactions that arranges elements in a vertical stack. This view is useful for creating lists or ordered sequences of elements where dragging and dropping can reorder or add new items within the stack.
SOURCE: [https://docs.jointjs.com/learn/features/drag-and-drop/stack-layout-view](https://docs.jointjs.com/learn/features/drag-and-drop/stack-layout-view)

LANGUAGE: Javascript
CODE:

```javascript
import { dia, shapes, ui } from '@joint/plus';

const graph = new dia.Graph({}, { cellNamespace: shapes });
const paper = new dia.Paper({
    el: document.getElementById('paper'),
    model: graph,
    width: 800,
    height: 600,
    gridSize: 10,
    drawGrid: true,
    background: { color: '#f8f8f8' },
    cellViewNamespace: shapes
});

const stackLayoutView = new ui.StackLayoutView({
    paper: paper,
    elements: [
        new shapes.standard.Rectangle({ size: { width: 100, height: 40 }, attrs: { label: { text: 'Item 1' } } }),
        new shapes.standard.Rectangle({ size: { width: 100, height: 40 }, attrs: { label: { text: 'Item 2' } } }),
        new shapes.standard.Rectangle({ size: { width: 100, height: 40 }, attrs: { label: { text: 'Item 3' } } })
    ],
    padding: 10
});

paper.el.appendChild(stackLayoutView.render().el);
stackLayoutView.layout(); // Arrange the elements in a stack
```

-----

TITLE: Tree Layout View (Drag & Drop) in JointJS
DESCRIPTION: The JointJS+ Tree Layout View is a component designed for drag and drop within a tree-like hierarchical structure. It enables users to interactively arrange and manage elements in a tree layout, making it suitable for representing organizational charts, file systems, or other hierarchical data structures.
SOURCE: [https://docs.jointjs.com/learn/features/drag-and-drop/tree-layout-view](https://docs.jointjs.com/learn/features/drag-and-drop/tree-layout-view)

LANGUAGE: Javascript
CODE:

```javascript
import { dia, shapes, ui } from '@joint/plus';

const graph = new dia.Graph({}, { cellNamespace: shapes });
const paper = new dia.Paper({
    el: document.getElementById('paper'),
    model: graph,
    width: 800,
    height: 600,
    gridSize: 10,
    drawGrid: true,
    background: { color: '#f8f8f8' },
    cellViewNamespace: shapes
});

const treeLayoutView = new ui.TreeLayoutView({
    paper: paper,
    elements: [
        new shapes.standard.Rectangle({ id: 'root', size: { width: 80, height: 30 }, attrs: { label: { text: 'Root' } } }),
        new shapes.standard.Rectangle({ id: 'child1', size: { width: 80, height: 30 }, attrs: { label: { text: 'Child 1' } } }),
        new shapes.standard.Rectangle({ id: 'child2', size: { width: 80, height: 30 }, attrs: { label: { text: 'Child 2' } } }),
    ],
    // For a tree, you'd typically define parent-child relationships via links or specific options
    // This is a simplified example; full tree layout requires graph structure.
});

// Add elements to the graph for layout to work on
graph.addCells(treeLayoutView.getElements());

// This example assumes manual positioning or a separate layout algorithm for actual tree structure.
// The TreeLayoutView is primarily for drag-drop interaction within a tree context.
```

-----

TITLE: Path Drawer (Vector Editor) in JointJS
DESCRIPTION: The JointJS+ Path Drawer is a feature within the Vector Editor that allows users to create custom vector paths interactively on the paper. It provides tools for drawing complex shapes and curves, offering fine-grained control over the geometry of path elements.
SOURCE: [https://docs.jointjs.com/learn/features/vector-editor/path-drawer](https://docs.jointjs.com/learn/features/vector-editor/path-drawer)

LANGUAGE: Javascript
CODE:

```javascript
import { dia, ui, shapes } from '@joint/plus';

const graph = new dia.Graph({}, { cellNamespace: shapes });
const paper = new dia.Paper({
    el: document.getElementById('paper'),
    model: graph,
    width: 800,
    height: 600,
    gridSize: 10,
    drawGrid: true,
    background: { color: '#f8f8f8' },
    cellViewNamespace: shapes
});

const pathDrawer = new ui.PathDrawer({ paper: paper });

paper.on('blank:pointerdown', (evt, x, y) => {
    // Start drawing a new path on blank paper click
    pathDrawer.startDrawing(x, y);
});

// Listen for path completion
pathDrawer.on('path:drawn', (path) => {
    const customPath = new shapes.standard.Path({
        d: path, // The SVG path string generated by PathDrawer
        attrs: {
            body: {
                stroke: 'blue',
                fill: 'lightblue',
                strokeWidth: 2
            }
        }
    });
    graph.addCell(customPath);
});
```

-----

TITLE: Path Editor (Vector Editor) in JointJS
DESCRIPTION: The JointJS+ Path Editor is a component of the Vector Editor that allows for precise modification of existing vector paths. It provides tools to manipulate the segments, points, and curves of a path, enabling detailed editing of complex graphical elements within a diagram.
SOURCE: [https://docs.jointjs.com/learn/features/vector-editor/path-editor](https://docs.jointjs.com/learn/features/vector-editor/path-editor)

LANGUAGE: Javascript
CODE:

```javascript
import { dia, ui, shapes } from '@joint/plus';

const graph = new dia.Graph({}, { cellNamespace: shapes });
const paper = new dia.Paper({
    el: document.getElementById('paper'),
    model: graph,
    width: 800,
    height: 600,
    gridSize: 10,
    drawGrid: true,
    background: { color: '#f8f8f8' },
    cellViewNamespace: shapes
});

// Create an example path to edit
const myPath = new shapes.standard.Path({
    d: 'M 10 10 L 100 10 L 100 100 L 10 100 Z', // A simple rectangle path
    attrs: {
        body: {
            stroke: 'green',
            fill: 'lightgreen',
            strokeWidth: 2
        }
    }
});
graph.addCell(myPath);

const pathEditor = new ui.PathEditor({ cellView: paper.findViewByModel(myPath) });

paper.on('element:pointerdblclick', (elementView) => {
    if (elementView.model.isLink()) return; // Path editor for elements, not links by default
    pathEditor.startEditing(elementView);
});
```

-----

TITLE: Tooltips in JointJS
DESCRIPTION: The JointJS+ Tooltip plugin allows you to display informative messages anywhere in the UI. These tooltips can be configured to appear on various elements, providing context-sensitive information to the user when they hover over or interact with parts of the diagram.
SOURCE: [https://docs.jointjs.com/learn/features/tooltips](https://docs.jointjs.com/learn/features/tooltips)

LANGUAGE: Javascript
CODE:

```javascript
import { ui } from '@joint/plus';

const tooltip = new ui.Tooltip({
    content: 'This is a JointJS+ tooltip.',
    target: document.getElementById('my-button'), // Example target
    direction: 'auto',
    animation: true
});

// To show the tooltip programmatically
// tooltip.show();
// To hide the tooltip
// tooltip.hide();
```

-----

TITLE: Context Toolbar (Popups & Menus) in JointJS
DESCRIPTION: The JointJS+ Context Toolbar provides a contextual menu that appears near an element, offering relevant tools and actions based on the selected element. It's an efficient way to provide quick access to frequently used operations without cluttering the main interface.
SOURCE: [https://docs.jointjs.com/learn/features/popups-and-menus/context-toolbar](https://docs.jointjs.com/learn/features/popups-and-menus/context-toolbar)

LANGUAGE: Javascript
CODE:

```javascript
import { dia, ui, shapes } from '@joint/plus';

const graph = new dia.Graph({}, { cellNamespace: shapes });
const paper = new dia.Paper({
    el: document.getElementById('paper'),
    model: graph,
    width: 800,
    height: 600,
    gridSize: 10,
    drawGrid: true,
    background: { color: '#f8f8f8' },
    cellViewNamespace: shapes
});

const rect = new shapes.standard.Rectangle({
    position: { x: 100, y: 100 },
    size: { width: 100, height: 50 },
    attrs: { label: { text: 'Click Me' } }
});
graph.addCell(rect);

paper.on('element:pointerclick', (elementView) => {
    const contextToolbar = new ui.ContextToolbar({
        target: elementView.el,
        tools: [
            { id: 'edit', content: 'Edit', action: () => alert('Edit clicked for ' + elementView.model.id) },
            { id: 'delete', content: 'Delete', action: () => elementView.model.remove() }
        ]
    });
    contextToolbar.render();
});
```

-----

TITLE: Dialog (Popups & Menus) in JointJS
DESCRIPTION: The JointJS+ Dialog component enables the creation of interactive modal dialogs for user input or confirmation. These pop-up windows are essential for gathering information, displaying alerts, or confirming actions within a JointJS application.
SOURCE: [https://docs.jointjs.com/learn/features/popups-and-menus/dialog](https://docs.jointjs.com/learn/features/popups-and-menus/dialog)

LANGUAGE: Javascript
CODE:

```javascript
import { ui } from '@joint/plus';

const dialog = new ui.Dialog({
    title: 'JointJS+ Dialog',
    content: 'This is a custom dialog message.',
    buttons: [
        { content: 'OK', action: 'ok', className: 'joint-button joint-primary-button' },
        { content: 'Cancel', action: 'cancel', className: 'joint-button' }
    ]
});

// Show the dialog
// dialog.open();

// Listen for button clicks
dialog.on('action:ok', () => {
    alert('OK button clicked!');
    dialog.close();
});

dialog.on('action:cancel', () => {
    alert('Cancel button clicked!');
    dialog.close();
});
```

-----

TITLE: Flash Message (Popups & Menus) in JointJS
DESCRIPTION: The JointJS+ Flash Message component provides a way to display temporary, non-intrusive notifications to the user. These messages are typically used for conveying quick feedback, such as successful operations or minor warnings, and usually disappear automatically after a short period.
SOURCE: [https://docs.jointjs.com/learn/features/popups-and-menus/flash-message](https://docs.jointjs.com/learn/features/popups-and-menus/flash-message)

LANGUAGE: Javascript
CODE:

```javascript
import { ui } from '@joint/plus';

// Show a success message
ui.FlashMessage.show('success', 'Operation successful!', {
    duration: 3000, // Message disappears after 3 seconds
    anchor: 'top-right'
});

// Show an error message
// ui.FlashMessage.show('error', 'An error occurred.', {
//     duration: 5000,
//     anchor: 'bottom-left'
// });
```

-----

TITLE: Lightbox (Popups & Menus) in JointJS
DESCRIPTION: The JointJS+ Lightbox component provides a modal overlay for displaying larger content, such as images or detailed information, while dimming the rest of the application. It's ideal for focusing user attention on specific content without navigating away from the current view.
SOURCE: [https://docs.jointjs.com/learn/features/popups-and-menus/lightbox](https://docs.jointjs.com/learn/features/popups-and-menus/lightbox)

LANGUAGE: Javascript
CODE:

```javascript
import { ui } from '@joint/plus';

const lightbox = new ui.Lightbox({
    image: 'https://docs.jointjs.com/img/jointjs-plus.png', // Example image
    title: 'JointJS+ Feature',
    closeButton: true
});

// To open the lightbox
// lightbox.open();
```

-----

TITLE: Popup (Popups & Menus) in JointJS
DESCRIPTION: The JointJS+ Popup component offers a flexible way to display custom content in a small, transient window that can be positioned relative to another element or at a specific coordinate. It is useful for displaying additional information, mini-forms, or interactive elements without interrupting the main workflow.
SOURCE: [https://docs.jointjs.com/learn/features/popups-and-menus/popup](https://docs.jointjs.com/learn/features/popups-and-menus/popup)

LANGUAGE: Javascript
CODE:

```javascript
import { ui } from '@joint/plus';

const myElement = document.getElementById('my-button'); // Assume an HTML element exists

const popup = new ui.Popup({
    target: myElement, // Element to anchor the popup to
    content: '<div>Hello from JointJS+ Popup!</div><input type="text" placeholder="Type here...">',
    position: 'auto', // Auto-positioning relative to target
    hideOn: ['pointerdown', 'escape'] // Hide when clicking outside or pressing escape
});

// To open the popup
// popup.open();
```

-----

TITLE: Color Palette (Form Controls) in JointJS
DESCRIPTION: The JointJS+ Color Palette is a form control that provides a visual selection of colors. It allows users to easily pick a color from a predefined set, simplifying color selection within diagram elements or application settings.
SOURCE: [https://docs.jointjs.com/learn/features/form-controls/color-palette](https://docs.jointjs.com/learn/features/form-controls/color-palette)

LANGUAGE: Javascript
CODE:

```javascript
import { ui } from '@joint/plus';

const colorPalette = new ui.ColorPalette({
    colors: ['#FF0000', '#00FF00', '#0000FF', '#FFFF00', '#FF00FF', '#00FFFF'],
    selected: '#FF0000'
});

document.getElementById('color-palette-holder').appendChild(colorPalette.render().el);

colorPalette.on('color:change', (color) => {
    console.log('Selected color:', color);
});
```

-----

TITLE: Radio Group (Form Controls) in JointJS
DESCRIPTION: The JointJS+ Radio Group is a form control that allows users to select one option from a predefined set of mutually exclusive choices. It's useful for providing clear, single-choice selections within configuration panels or element properties.
SOURCE: [https://docs.jointjs.com/learn/features/form-controls/radio-group](https://docs.jointjs.com/learn/features/form-controls/radio-group)

LANGUAGE: Javascript
CODE:

```javascript
import { ui } from '@joint/plus';

const radioGroup = new ui.RadioGroup({
    name: 'myRadioGroup',
    options: [
        { value: 'option1', content: 'Option A' },
        { value: 'option2', content: 'Option B' },
        { value: 'option3', content: 'Option C' }
    ],
    selected: 'option2'
});

document.getElementById('radio-group-holder').appendChild(radioGroup.render().el);

radioGroup.on('change', (value) => {
    console.log('Selected option:', value);
});
```

-----

TITLE: Select Box (Form Controls) in JointJS
DESCRIPTION: The JointJS+ Select Box is a form control that provides a dropdown list for users to choose from a set of options. It's commonly used in property editors or forms to allow selection from a potentially long list of choices in a compact manner.
SOURCE: [https://docs.jointjs.com/learn/features/form-controls/select-box](https://docs.jointjs.com/learn/features/form-controls/select-box)

LANGUAGE: Javascript
CODE:

```javascript
import { ui } from '@joint/plus';

const selectBox = new ui.SelectBox({
    options: [
        { value: 'apple', content: 'Apple' },
        { value: 'banana', content: 'Banana' },
        { value: 'cherry', content: 'Cherry' }
    ],
    selected: 'banana'
});

document.getElementById('select-box-holder').appendChild(selectBox.render().el);

selectBox.on('change', (value) => {
    console.log('Selected value:', value);
});
```

-----

TITLE: Select Button Group (Form Controls) in JointJS
DESCRIPTION: The JointJS+ Select Button Group is a form control that presents a set of buttons, where selecting one button automatically deselects others in the group. This provides a clear and interactive way for users to make a single choice from a set of visually distinct options.
SOURCE: [https://docs.jointjs.com/learn/features/form-controls/select-button-group](https://docs.jointjs.com/learn/features/form-controls/select-button-group)

LANGUAGE: Javascript
CODE:

```javascript
import { ui } from '@joint/plus';

const selectButtonGroup = new ui.SelectButtonGroup({
    options: [
        { value: 'left', content: 'Left' },
        { value: 'center', content: 'Center' },
        { value: 'right', content: 'Right' }
    ],
    selected: 'center'
});

document.getElementById('button-group-holder').appendChild(selectButtonGroup.render().el);

selectButtonGroup.on('change', (value) => {
    console.log('Selected alignment:', value);
});
```

-----

TITLE: Themes and Styling in JointJS
DESCRIPTION: JointJS+ supports themes and styling, allowing you to customize the visual appearance of your diagrams and UI components. This feature provides flexibility in aligning the look and feel of your JointJS application with your brand or specific design requirements.
SOURCE: [https://docs.jointjs.com/learn/features/themes-and-styling/themes](https://docs.jointjs.com/learn/features/themes-and-styling/themes)

LANGUAGE: CSS
CODE:

```css
/* Example of a custom theme applied to paper and elements */
.joint-paper {
    background-color: #f0f0f0;
    border: 1px solid #ccc;
}

.joint-element.joint-type-standard-rectangle .joint-body {
    fill: #a2d2ff;
    stroke: #337ab7;
    stroke-width: 2px;
}
```

-----

TITLE: Local Storage in JointJS
DESCRIPTION: The JointJS+ Local Storage feature enables the ability to store JointJS graphs and cells directly in the client-side HTML5 `localStorage`. This allows for persistence of diagram data across browser sessions, ensuring that user work is saved even if the tab is refreshed or closed.
SOURCE: [https://docs.jointjs.com/learn/features/local-storage](https://docs.jointjs.com/learn/features/local-storage)

LANGUAGE: Javascript
CODE:

```javascript
import { dia, shapes, ui } from '@joint/plus';

const graph = new dia.Graph({}, { cellNamespace: shapes });
const paper = new dia.Paper({
    el: document.getElementById('paper'),
    model: graph,
    width: 800,
    height: 600,
    gridSize: 10,
    drawGrid: true,
    background: { color: '#f8f8f8' },
    cellViewNamespace: shapes
});

const localStorageManager = new ui.LocalStorage({
    graph: graph,
    paper: paper,
    storageKey: 'myJointJSGraph' // Unique key for your application
});

// To save the graph to local storage
// localStorageManager.save();

// To load the graph from local storage (e.g., on page load)
// localStorageManager.load();

// You can also clear the storage
// localStorageManager.clear();
```

-----

TITLE: Playwright Testing with JointJS
DESCRIPTION: JointJS+ provides guidance and support for testing your diagramming applications using Playwright. This enables robust end-to-end testing, ensuring that your JointJS features and user interactions behave as expected across different browsers.
SOURCE: [https://docs.jointjs.com/learn/testing/playwright](https://docs.jointjs.com/learn/testing/playwright)

LANGUAGE: Javascript
CODE:

```javascript
// Example Playwright test snippet (simplified)
// This code would typically be part of a Playwright test file (.spec.js or .test.js)

const { test, expect } = require('@playwright/test');

test('JointJS paper loads correctly', async ({ page }) => {
  await page.goto('http://localhost:3000/your-jointjs-app'); // Replace with your app's URL

  // Expect a title "to contain" a substring.
  await expect(page).toHaveTitle(/JointJS/);

  // Expect the JointJS paper element to be visible
  await expect(page.locator('.joint-paper')).toBeVisible();

  // You can add more specific tests here, e.g., checking for elements
  // await expect(page.locator('.joint-element')).toHaveCount(1);
});
```

-----

TITLE: Jest Testing with JointJS
DESCRIPTION: JointJS+ supports integration with Jest for unit and integration testing of your application's logic. Jest provides a powerful and convenient framework for testing JavaScript code, including components that interact with JointJS models and views.
SOURCE: [https://docs.jointjs.com/learn/testing/jest](https://docs.jointjs.com/learn/testing/jest)

LANGUAGE: Javascript
CODE:

```javascript
// Example Jest test snippet (simplified)
// This code would typically be part of a Jest test file (.test.js)

import { dia, shapes } from '@joint/plus';

describe('JointJS Graph operations', () => {
  let graph;

  beforeEach(() => {
    graph = new dia.Graph({}, { cellNamespace: shapes });
  });

  test('should add an element to the graph', () => {
    const rectangle = new shapes.standard.Rectangle();
    graph.addCell(rectangle);
    expect(graph.getElements()).toHaveLength(1);
    expect(graph.getCell(rectangle.id)).toBe(rectangle);
  });

  test('should remove an element from the graph', () => {
    const rectangle = new shapes.standard.Rectangle();
    graph.addCell(rectangle);
    graph.removeCells([rectangle]);
    expect(graph.getElements()).toHaveLength(0);
  });
});
```
