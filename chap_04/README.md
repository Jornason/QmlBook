
http://qmlbook.org/ch04/index.html


# QML Syntax

In its simplest way QML is a hierarchy of elements. Child elements inherit the
coordinate system from the parent. A x,y coordinate is always relative to the
parent.

See example: rectangle


Elements are declared by using their element name but are defined by using their
properties or by creating custom properties. A property is a simple key-value
pair, e.g. width : 100, text: 'Greetings', color: '#FF0000'. A property has a
well-defined type and can have an initial value.


### Properties

<!-- code start -->
Text {
    // (1) identifier
    id: thisLabel

    // (2) set x- and y-position
    x: 24; y: 16

    // (3) bind height to 2 * width
    height: 2 * width

    // (4) custom property
    property int times: 24

    // (5) property alias
    property alias anotherTimes: thisLabel.times

    // (6) set text appended by value
    text: "Greetings " + times

    // (7) font is a grouped property
    font.family: "Ubuntu"
    font.pixelSize: 24

    // (8) KeyNavigation is an attached property
    KeyNavigation.tab: otherLabel

    // (9) signal handler for property changes
    onHeightChanged: console.log('height:', height)

    // focus is neeed to receive key events
    focus: true

    // change color based on focus value
    color: focus?"red":"black"

}
<!-- code end -->


Let’s go through the different features of properties:

1. id is a very special property-like value, it is used to reference elements
   inside a QML file (called document in QML). The id is not a string type but
   rather an identifier and part of the QML syntax. An id needs to be unique
   inside a document and it can’t be re-set to a different value, neither be
   queried. (It behaves more like a pointer in the C++ world.)

2. A property can be set to a value, depending on its type. If no value is given
   for a property, an initial value will be chosen. You need to consult the
   documentation of the particular element for more information about the
   initial value of a property.

3. A property can depend on one or many other properties. This is called
   binding. A bound property is updated, when its dependent properties change.
   It works like a contract, in this case the height should always be two times
   the width.

4. Adding own properties to an element is done using the property qualifier
   followed by the type, the name and the optional initial value (property
   <type> <name> : <value>). If no initial value is given a system initial value
   is chosen.

5. Another important way of declaring properties is using the alias keyword
   (property alias <name> : <reference>). The alias keyword allows us to forward
   a property of an object or an object itself from within the type to an outer
   scope. We will use this technique later when defining components to export
   the inner properties or element ids to the root level. A property alias does
   not need a type, it uses the type of the referenced property or object.

6. The text property depends on the custom property times of type int. The int
   based value is automatically converted to a string type. The expression
   itself is another example of binding and results into the text being updated
   every time the times property changes.

7. Some properties are grouped properties. This feature is used when a property
   is more structured and related properties should be grouped together. Another
   way of writing grouped properties is font { family: "Ubuntu"; pixelSize: 24 }.

8. Some properties are attached to the element itself. This is done for global
   relevant elements which appear only once in the application (e.g. keyboard
   input). The writing is <Element>.<property>: <value>.

9. For every property you can provide an signal handler. This handler is called
   after the property changes. For example here we want to be notified whenever
   the height changes and use the built-in console to log a message to the
   system.


An element id should only be used to reference elements inside your document
(e.g. the current file). 


### Scripting

QML and JavaScript (also known as EcmaScript) are best friends. In the
JavaScript chapter we will go into more detail on this symbiosis. Currently we
just want to make you aware about this relationship.


<!-- code start -->
Text {
    id: label

    x: 24; y: 24

    // custom counter property for space presses
    property int spacePresses: 0

    text: "Space pressed: " + spacePresses + " times"

    // (1) handler for text changes
    onTextChanged: console.log("text changed to:", text)

    // need focus to receive key events
    focus: true

    // (2) handler with some JS
    Keys.onSpacePressed: {
        increment()
    }

    // clear the text on escape
    Keys.onEscapePressed: {
        label.text = ''
    }

    // (3) a JS function
    function increment() {
        spacePresses = spacePresses + 1
     }

}
<!-- code end -->


Definition of a JavaScript function in the form of
function <name>(<parameters>) { ... },
which increments our counter spacePressed. Every time spacePressed is
incremented bound properties will also be updated.


--------------------------------------------------------------------------------

# Basic Elements


Elements can be grouped into visual and non-visual elements. A visual element
(like the Rectangle) has a geometry and normally present an area on the screen.
A non-visual element (like a Timer) provides general functionality, normally
used to manipulate the visual elements.

Currently we will focus on the fundamental visual elements, such as Item,
Rectangle, Text, Image and MouseArea.


### Item Element

Item is the base element for all visual elements as such all other visual
elements inherit from Item. It doesn’t paint anything by itself but defines all
properties which are common across all visual elements:

Geometry
Layout handling
Key handling
Transformation
Visual
State definition


The Item element is often used as a container for other elements, similar to the
div element in HTML.


### Rectangle element

The Rectangle extends Item and adds a fill color to it. Additional it supports
borders defined by border.color and border.width. To create rounded rectangles
you can use the radius property.

The named colors used are colors from the SVG color names
(see http://www.w3.org/TR/css3-color/#svg-color). You can provide colors in QML
in different ways the most common ways are as RGB string (‘#FF4444’) or as a
color name (e.g. ‘white’).


--------------------------------------------------------------------------------

# Components

A file based component is created by placing a QML element in a file and give
the file an element name (e.g. Button.qml). You can use the component like every
other element from the QtQuick module, in our case you would use this in your
code as Button { ... }.









