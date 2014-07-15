
# Meet Qt5

http://qmlbook.org/ch01/index.html


Qt 5 is focused on the the following:

- Outstanding Graphics: Qt Quick 2 is based on OpenGL (ES) using a scene graph
implementation. The recomposed graphics stack allows a new level of graphic
effects combined with an ease of use never seen before in this field.

- Developer Productivity: QML and JavaScript are the primary means for UI
creation. The back-end will be driven by C++. The split between JavaScript and
C++ allows a fast iteration for front-end developers concentrating on creating
beautiful user interfaces and back-end C++ developers concentrating on
stability, performance and extending the runtime.

- Cross-platform portability: With the consolidated Qt Platform Abstraction, it
is now possible to port Qt to a wider range of platforms easier and faster. Qt 5
is structured around the concept of Qt Essentials and Add-ons, which allows OS
developer to focus on the essentials modules and leads to a smaller runtime
altogether.

- Open Development: Qt is now a truly open-governance project hosted at
Qt-Project. The development is open and community driven.

--------------------------------------------------------------------------------

Qt Quick is the umbrella term for the user interface technology used in Qt5. 
Qt Quick itself is a collection of several technologies:

QML - Markup language for user interfaces
JavaScript - The dynamic scripting language
Qt C++ - The highly portable enhanced c++ library

Similar to HTML, QML is a markup language. In a typical project the front-end
is developed in QML/JavaScript and the back-end code, which interfaces with the
system and does the heavy lifting is developed using Qt C++.

--------------------------------------------------------------------------------

Example:

Let’s create a simple user interface using QtQuick, which showcases some aspects
of the QML language. At the end we will have a paper windmill with rotating
blades.

(Open Qt Creator and create a Qt Quick UI Project:
 File -> New File or Project -> Qt Quick UI )

We start with an empty document called main.qml. All QML files will have the
ending .qml. As a markup language (like HTML) a QML document needs to have one
and only one root element, which in our case is the Image element with a width
and height based on the background image geometry:

<!-- code start -->
import QtQuick 2.0

Image {
    id: root
    source: "images/background.png"
}
<!-- code end -->

Please see windmill example.









