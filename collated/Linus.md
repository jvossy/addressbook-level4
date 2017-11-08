# Linus
###### \out\production\resources\view\default.html
``` html
<html>
<title>Home Page</title>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no">
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.2/css/bootstrap.min.css" integrity="sha384-PsH8R72JQ3SOdhVi3uxftmaW6Vc51MKb0q5P2rRUpPvrszuE4W1povHYgTpBfshb" crossorigin="anonymous">

<style type="text/css">
    html {
        height: 100%;
        width: 100%;
    }

    body {
        height: 100%;
        width: 100%;
        margin: 0px;
        padding: 0px
    }

    img {
        user-drag: none;
        user-select: none;
        -moz-user-select: none;
        -webkit-user-drag: none;
        -webkit-user-select: none;
        -ms-user-select: none;
    }

    strong {
        font-size: 18px;
    }
    p {
        word-break: break-all;
    }

    .container{
        margin: 0px;
        padding: 0px;
        height: 100%;
    }
    .row{
        margin: 0px;
        padding: 0px;
        height: 100%;
    }
</style>

<body>

<!-- First Grid: Picture & Contact Info -->
<div class="row">
    <div class="card col-4">
        <img class="card-img-top" src="../images/bg.jpeg" alt="Card image cap">
        <div class="card-body">

            <strong>
                <h3>Project Name: Unibook</h3>
                <h3>Current Version: <span class='badge badge-warning'>v1.4</span></h3>
                <p>License: <span class='badge badge-info'>MIT</span> Build: <span class='badge badge-success'>passing</span> codacy: <span class='badge badge-primary'>A</span></p>
                <p>UI Design: Linus, Vos</p>
                <p>Function implement: Sirisha, Henning</p>
                <p>Tutorial: T13-B2</p>
                <p>Last updated: 2017/11/02</p>
            </strong>

        </div>
    </div>

    <div class="jumbotron jumbotron-fluid col-8" style="padding: 20px; background: #f7f7f7">
        <h1 style="text-align: center"><b>Unibook Commands</b></h1>

        <div class="card border-primary mb-3">
            <div class="card-header">Home command</div>
            <div class="card-body text-primary">
                <h4 class="card-title">Goes back to the home panel. </h4>
            </div>
        </div>

        <div class="card border-success mb-3">
            <div class="card-header">Add command</div>
            <div class="card-body text-success">
                <h4 class="card-title">Adds a person to the address book. </h4>
                <p class="card-text">Parameters: n/NAME p/PHONE e/EMAIL a/ADDRESS [s/SCORE] [t/TAG]...</p>
            </div>
        </div>
        <div class="card border-secondary mb-3">
            <div class="card-header">Delete command</div>
            <div class="card-body text-secondary">
                <h4 class="card-title">Deletes the person identified by the index number used in the last person listing.</h4>
                <p class="card-text">Parameters: INDEX (must be a positive integer)</p>
            </div>
        </div>

        <div class="card border-success mb-3">
            <div class="card-header">Find command</div>
            <div class="card-body text-success">
                <h4 class="card-title">Finds persons whose names contain any of the given keywords.</h4>
                <p class="card-text">Parameters: find KEYWORD [MORE_KEYWORDS]...</p>
            </div>
        </div>
        <div class="card border-danger mb-3">
            <div class="card-header">Clear command</div>
            <div class="card-body text-danger">
                <h4 class="card-title">Clears all entries from the address book.</h4>
            </div>
        </div>
        <div class="card border-warning mb-3">
            <div class="card-header">Undo command</div>
            <div class="card-body text-warning">
                <h4 class="card-title">Restores the address book to the state before the previous undoable command was executed.</h4>
            </div>
        </div>
        <div class="card border-secondary mb-3">
            <div class="card-header">Redo command</div>
            <div class="card-body text-info">
                <h4 class="card-title">Reverses the most recent undo command.</h4>
            </div>
        </div>

    </div>

</div>
</body>
</html>
```
###### \out\production\resources\view\LightTheme.css
``` css
.root {
    -fx-accent: derive(#f7f5f4, -10%);
    -fx-focus-color: derive(#f7f5f4, -10%);
}

.background {
    -fx-background-color: #f7f7f7;
    background-color: #f7f7f7; /* Used in the default.html file */
}

.v-box {
    -fx-background-color:  #f7f7f7;
}

.label {
    -fx-font-size: 11pt;
    -fx-font-family: "Segoe UI Semibold";
    -fx-text-fill: #000000;
    -fx-opacity: 0.9;
}

.label-bright {
    -fx-font-size: 11pt;
    -fx-font-family: "Segoe UI Semibold";
    -fx-text-fill: gray;
    -fx-opacity: 1;
}

.label-header {
    -fx-font-size: 32pt;
    -fx-font-family: "Segoe UI Light";
    -fx-text-fill: gray;
    -fx-opacity: 1;
}

.text-field {
    -fx-font-size: 12pt;
    -fx-font-family: "Segoe UI Semibold";
}

.tab-pane {
    -fx-padding: 0 0 0 1;
}

.tab-pane .tab-header-area {
    -fx-padding: 0 0 0 0;
    -fx-min-height: 0;
    -fx-max-height: 0;
}

.table-view {
    -fx-base: #f7f7f7;
    -fx-control-inner-background:  #f7f7f7;
    -fx-background-color: #f7f7f7;
    -fx-table-cell-border-color: transparent;
    -fx-table-header-border-color: transparent;
    -fx-padding: 5;
}

.table-view .column-header-background {
    -fx-background-color: transparent;
}

.table-view .column-header, .table-view .filler {
    -fx-size: 35;
    -fx-border-width: 0 0 1 0;
    -fx-background-color: transparent;
    -fx-border-color:
        transparent
        transparent
        derive(-fx-base, 80%)
        transparent;
    -fx-border-insets: 0 10 1 0;
}

.table-view .column-header .label {
    -fx-font-size: 20pt;
    -fx-font-family: "Segoe UI Light";
    -fx-text-fill: gray;
    -fx-alignment: center-left;
    -fx-opacity: 1;
}

.table-view:focused .table-row-cell:filled:focused:selected {
    -fx-background-color: -fx-focus-color;
}

.split-pane:horizontal .split-pane-divider {
    -fx-background-color: transparent;
    -fx-border-color: transparent;
}

.split-pane {
    -fx-border-radius: 1;
    -fx-border-width: 1;
    -fx-background-color: transparent;
}

.list-view {
    -fx-background-insets: 0;
    -fx-padding: 0;
}

.list-cell {
    -fx-label-padding: 0 0 0 0;
    -fx-graphic-text-gap : 0;
    -fx-padding: 0 0 0 0;
}

.list-cell:filled:even {
    -fx-background-color: #ffffff;
}

.list-cell:filled:odd {
    -fx-background-color: #ffffff;
}

.list-cell:filled:selected {
    -fx-background-color: derive(#f7f5f4, -5%);
}

.list-cell:filled:selected #cardPane {
    -fx-border-color: transparent;
    -fx-border-width: 1;
}

.cell_big_label {
    -fx-font-family: "Segoe UI Semibold";
    -fx-font-size: 16px;
    -fx-text-fill: #444344;
}

.cell_id_label {
    -fx-font-family: "Segoe UI Semibold";
    -fx-text-fill: derive(gray, 35%);
    -fx-font-size: 15px;
}

.person_big_label {
    -fx-font-family: "Segoe UI Semibold";
    -fx-font-size: 26px;
    -fx-text-fill: #444344;
}

.person_small_label {
    -fx-font-family: "Lucida Grande", "Segoe UI", Optima;
    -fx-font-size: 15px;
    -fx-text-fill: #848484;
}

.anchor-pane {
     -fx-background-color: transparent;
}

.pane-with-border {
     -fx-background-color: transparent;
     -fx-border-top-width: 1px;
}

.result-pane {
     -fx-background-color: #ffffff;
     -fx-effect: dropshadow(gaussian, derive(#f7f5f4, -15%), 10, 0, 2, 2);
}

.person-detail-panel {
    -fx-background-color: #ffffff;
    -fx-effect: dropshadow(gaussian, derive(#f7f5f4, -15%), 10, 0, 2, 2);
}

.person-vbox {
    -fx-effect: dropshadow(gaussian, derive(#f7f5f4, -15%), 10, 0, -2, 2);
}

.status-bar {
    -fx-background-color: derive(#f7f5f4, 80%);
    -fx-padding: 0 10 0 10;
}

.result-display {
    -fx-background-color: transparent;
    -fx-font-family: "Segoe UI Light";
    -fx-font-size: 12pt;
    -fx-text-fill: gray;
}

.status-bar .label {
    -fx-font-family: "Segoe UI Light";
    -fx-text-fill: derive(#716f70, -10%);
    -fx-font-size: 13px;
}

.status-bar-with-border {
    -fx-background-color: derive(#f7f5f4, 30%);
    -fx-border-color: derive(#f7f5f4, 25%);
    -fx-border-width: 1px;
}

.status-bar-with-border .label {
    -fx-text-fill: gray;
}

.grid-pane {
    -fx-background-color: derive(#f7f5f4, 30%);
    -fx-border-color: derive(#f7f5f4, 30%);
    -fx-border-width: 1px;
}

.grid-pane .anchor-pane {
    -fx-background-color: derive(#f7f5f4, 80%);
}

.context-menu {
    -fx-background-color: derive(#f7f5f4, 50%);
}

.context-menu .label {
    -fx-text-fill: gray;
}

.menu-bar {
    -fx-background-color: derive(#f7f5f4, 80%);
}

.menu-bar .label {
    -fx-font-size: 12pt;
    -fx-font-family: "Segoe UI Light";
    -fx-text-fill: derive(#716f70, -10%);
    -fx-opacity: 0.9;
}

.menu .left-container {
    -fx-background-color: black;
}

/*
 * Metro style Push Button
 * Author: Pedro Duque Vieira
 * http://pixelduke.wordpress.com/2012/10/23/jmetro-windows-8-controls-on-java/
 */
.button {
    -fx-padding: 5 22 5 22;
    -fx-border-color: #e2e2e2;
    -fx-border-width: 2;
    -fx-background-radius: 0;
    -fx-background-color: #f7f5f4;
    -fx-font-family: "Segoe UI", Optima, Helvetica, Arial, sans-serif;
    -fx-font-size: 11pt;
    -fx-text-fill: #d8d8d8;
    -fx-background-insets: 0 0 0 0, 0, 1, 2;
}

.button:hover {
    -fx-background-color: #3a3a3a;
}

.button:pressed, .button:default:hover:pressed {
  -fx-background-color: gray;
  -fx-text-fill: #f7f5f4;
}

.button:focused {
    -fx-border-color: gray, gray;
    -fx-border-width: 1, 1;
    -fx-border-style: solid, segments(1, 1);
    -fx-border-radius: 0, 0;
    -fx-border-insets: 1 1 1 1, 0;
}

.button:disabled, .button:default:disabled {
    -fx-opacity: 0.4;
    -fx-background-color: #f7f5f4;
    -fx-text-fill: gray;
}

.button:default {
    -fx-background-color: -fx-focus-color;
    -fx-text-fill: slategrey;
}

.button:default:hover {
    -fx-background-color: derive(-fx-focus-color, 30%);
}

.dialog-pane {
    -fx-background-color: #f7f5f4;
}

.dialog-pane > *.button-bar > *.container {
    -fx-background-color: #f7f5f4;
}

.dialog-pane > *.label.content {
    -fx-font-size: 14px;
    -fx-font-weight: bold;
    -fx-text-fill: gray;
}

.dialog-pane:header *.header-panel {
    -fx-background-color: derive(#f7f5f4, 25%);
}

.dialog-pane:header *.header-panel *.label {
    -fx-font-size: 18px;
    -fx-font-style: italic;
    -fx-fill: gray;
    -fx-text-fill: gray;
}

.scroll-bar {
    -fx-background-color: derive(#f7f5f4, -5%);
}

.scroll-bar .thumb {
    -fx-background-color: derive(#f7f5f4, -25%);
    -fx-background-insets: 1;
    -fx-background-radius: 18 18 18 18;
}

.scroll-bar .increment-button, .scroll-bar .decrement-button {
    -fx-background-color: transparent;
    -fx-padding: 0 0 0 0;
}

.scroll-bar .increment-arrow, .scroll-bar .decrement-arrow {
    -fx-shape: " ";
}

.scroll-bar:vertical .increment-arrow, .scroll-bar:vertical .decrement-arrow {
    -fx-padding: 5 3 5 3;
}

.scroll-bar:horizontal .increment-arrow, .scroll-bar:horizontal .decrement-arrow {
    -fx-padding: 3 5 3 5;
}

#cardPane {
    -fx-background-color: transparent;
    -fx-border-width: 0;
}
/*
#avatarImage {
    -fx-image: url("../images/avatarGray.png");
}
*/
#phone {
    -fx-image: url("../images/phone.png");
}

#initial_small {
    -fx-font-family: "Roboto";
    -fx-text-fill: #ffffff;
    -fx-font-size: 25px;
}

#initial_big {
    -fx-font-family: "Roboto";
    -fx-text-fill: #ffffff;
    -fx-font-size: 45px;
}

#commandTypeLabel {
    -fx-font-size: 11px;
    -fx-text-fill: #f70d1a;
}

#commandTextField {
    -fx-background-color: transparent;
    -fx-background-insets: 0;
    -fx-border-insets: 0;
    -fx-border-width: 1;
    -fx-font-family: "Segoe UI Light";
    -fx-font-size: 13pt;
    -fx-text-fill: gray;
}

.command-pane {
    -fx-background-color: #ffffff;
    -fx-background-radius: 18 18 18 18;
    -fx-effect: dropshadow(gaussian, derive(#f7f5f4, -15%), 10, 0, 1, 2);
}

#filterField, #personListPanel {
    -fx-effect: innershadow(gaussian, black, 10, 0, 0, 0);
}

#resultDisplay .content {
    -fx-background-color: transparent, #ffffff, transparent, #ffffff;
    -fx-background-radius: 0;
}

#tags {
    -fx-hgap: 7;
    -fx-vgap: 3;
}

#tags .label {
    -fx-font-family: "Segoe UI", Optima;
    -fx-text-fill: white;
    -fx-padding: 1 0 1 0;
    -fx-font-size: 14px;
}
```
###### \out\production\resources\view\StatusBarFooter.fxml
``` fxml
        <?import org.controlsfx.control.StatusBar?>
        <?import javafx.scene.layout.ColumnConstraints?>
        <?import javafx.scene.layout.GridPane?>

<GridPane styleClass="grid-pane" xmlns="http://javafx.com/javafx/8" xmlns:fx="http://javafx.com/fxml/1">
<columnConstraints>
  <ColumnConstraints hgrow="SOMETIMES" minWidth="10" prefWidth="100" />
  <ColumnConstraints hgrow="SOMETIMES" minWidth="10" prefWidth="100" />
</columnConstraints>
<StatusBar styleClass="anchor-pane" fx:id="syncStatus" />
<StatusBar styleClass="anchor-pane" fx:id="saveLocationStatus" GridPane.columnIndex="1" nodeOrientation="RIGHT_TO_LEFT" />
</GridPane>
```
###### \out\production\resources\view\StatusBarFooter.fxml
``` fxml

```
###### \src\main\java\seedu\address\commons\events\ui\BrowserJumpToHomePage.java
``` java
package seedu.address.commons.events.ui;

import java.net.URL;

import seedu.address.commons.events.BaseEvent;

/**
 * Represents the view change in the browser panel
 */
public class BrowserJumpToHomePage extends BaseEvent {

    private URL url;

    public BrowserJumpToHomePage(URL url) {
        this.url = url;
    }

    @Override
    public String toString() {
        return this.getClass().getSimpleName();
    }

    public URL getHomeUrl() {
        return url;
    }

}
```
###### \src\main\java\seedu\address\commons\events\ui\PersonPanelSelectionChangedEvent.java
``` java
    private final int backToHomePageValue = 0;
```
###### \src\main\java\seedu\address\commons\events\ui\PersonPanelSelectionChangedEvent.java
``` java

    public PersonPanelSelectionChangedEvent(PersonCard newSelection) {
        this.newSelection = newSelection;
    }

    @Override
    public String toString() {
        return this.getClass().getSimpleName();
    }

    public PersonCard getNewSelection() {
        return newSelection;
    }

```
###### \src\main\java\seedu\address\commons\events\ui\PersonPanelSelectionChangedEvent.java
``` java
    public int getBackToHomePageValue() {
        return this.backToHomePageValue;
    }
```
###### \src\main\java\seedu\address\commons\events\ui\PersonPanelSelectionChangedEvent.java
``` java

}
```
###### \src\main\java\seedu\address\logic\commands\HomeCommand.java
``` java
package seedu.address.logic.commands;

import static seedu.address.model.Model.PREDICATE_SHOW_ALL_PERSONS;
import static seedu.address.ui.BrowserPanel.DEFAULT_PAGE;
import static seedu.address.ui.UiPart.FXML_FILE_FOLDER;

import java.net.URL;

import seedu.address.MainApp;
import seedu.address.commons.core.EventsCenter;
import seedu.address.commons.events.ui.BrowserJumpToHomePage;

/**
 * Goes back to home page
 */
public class HomeCommand extends Command {

    public static final String COMMAND_WORD = "home";

    public static final String MESSAGE_SUCCESS = "Successfully went back to home page";

    @Override
    public CommandResult execute() {
        model.changeListTo(COMMAND_WORD);
        model.updateFilteredPersonList(PREDICATE_SHOW_ALL_PERSONS);

        URL url = MainApp.class.getResource(FXML_FILE_FOLDER + DEFAULT_PAGE);
        EventsCenter.getInstance().post(new BrowserJumpToHomePage(url));

        return new CommandResult(MESSAGE_SUCCESS);
    }

}
```
###### \src\main\java\seedu\address\logic\commands\HomeCommand.java
``` java

```
###### \src\main\java\seedu\address\logic\parser\AddressBookParser.java
``` java
        case HomeCommand.COMMAND_WORD:
            return new HomeCommand();
```
###### \src\main\java\seedu\address\logic\parser\AddressBookParser.java
``` java

        case ListCommand.COMMAND_WORD:
        case ListCommand.COMMAND_WORD_ALIAS:
            return new ListCommand();

        case HistoryCommand.COMMAND_WORD:
        case HistoryCommand.COMMAND_WORD_ALIAS:
            return new HistoryCommand();

        case ExitCommand.COMMAND_WORD:
            return new ExitCommand();

        case HelpCommand.COMMAND_WORD:
            return new HelpCommand();

        case UndoCommand.COMMAND_WORD:
        case UndoCommand.COMMAND_WORD_ALIAS:
            return new UndoCommand();

        case RedoCommand.COMMAND_WORD:
        case RedoCommand.COMMAND_WORD_ALIAS:
            return new RedoCommand();

        default:
            throw new ParseException(MESSAGE_UNKNOWN_COMMAND);
        }
    }

}

```
###### \src\main\java\seedu\address\ui\BrowserPanel.java
``` java
    public static final String BROWSER_PAGE = "BrowserPanel.html";
```
###### \src\main\java\seedu\address\ui\BrowserPanel.java
``` java
    public static final String GOOGLE_SEARCH_URL_PREFIX = "https://www.google.com.sg/search?safe=off&q=";
    public static final String GOOGLE_SEARCH_URL_SUFFIX = "&cad=h";

    private static final String FXML = "BrowserPanel.fxml";

    private final Logger logger = LogsCenter.getLogger(this.getClass());

```
###### \src\main\java\seedu\address\ui\BrowserPanel.java
``` java
    private int backToHomePage = 0;
```
###### \src\main\java\seedu\address\ui\BrowserPanel.java
``` java

    @FXML
    private WebView browser;

    public BrowserPanel() {
        super(FXML);

        // To prevent triggering events for typing inside the loaded Web page.
        getRoot().setOnKeyPressed(Event::consume);

        loadDefaultPage();
        registerAsAnEventHandler(this);
    }

    private void loadPersonPage(ReadOnlyPerson person) {
        loadPage(GOOGLE_SEARCH_URL_PREFIX + person.getName().fullName.replaceAll(" ", "+")
                + GOOGLE_SEARCH_URL_SUFFIX);
    }

    /**
     * Loads the located address page of the user's address.
     */
    private void loadBrowserPage(ReadOnlyPerson person) throws IOException {
```
###### \src\main\java\seedu\address\ui\BrowserPanel.java
``` java
        URL addressPage = MainApp.class.getResource(FXML_FILE_FOLDER + BROWSER_PAGE);
```
###### \src\main\java\seedu\address\ui\BrowserPanel.java
``` java
        loadPage(addressPage.toExternalForm());
    }


    public void loadPage(String url) {
        Platform.runLater(() -> browser.getEngine().load(url));
    }

    /**
     * Loads a default HTML file with a background that matches the general theme.
     */
    public void loadDefaultPage() {
        URL defaultPage = MainApp.class.getResource(FXML_FILE_FOLDER + DEFAULT_PAGE);
        loadPage(defaultPage.toExternalForm());
    }

    /**
     * Frees resources allocated to the browser.
     */
    public void freeResources() {
        browser = null;
    }

```
###### \src\main\java\seedu\address\ui\BrowserPanel.java
``` java
    @Subscribe
    private void handlePersonPanelSelectionChangedEvent(PersonPanelSelectionChangedEvent event) throws IOException {

        logger.info(LogsCenter.getEventHandlingLogMessage(event));
        ReadOnlyPerson p = event.getNewSelection().person;

        String address = p.getAddress().toString();
        String name = p.getName().toString();
        String emails = p.getEmail().toString();
        String phones = p.getPhone().toString();
        String tags = p.getOnlyTags().toString();

        backToHomePage = event.getBackToHomePageValue();

        browser.getEngine().getLoadWorker().stateProperty().addListener((obs, oldState, newState) -> {
            if (newState == Worker.State.SUCCEEDED && backToHomePage == 0) {
                WebEngine panel = browser.getEngine();
                panel.executeScript("document.setName(\"" + name + "\")");
                panel.executeScript("document.setAddress(\"" + address + "\")");
                panel.executeScript("document.setEmail(\"" + emails + "\")");
                panel.executeScript("document.setPhone(\"" + phones + "\")");
                panel.executeScript("document.setTags(\"" + tags + "\")");

            }
        });

        loadBrowserPage(event.getNewSelection().person);

    }

    @Subscribe
    private void handleGoBackToHomePageEvent(BrowserJumpToHomePage event) throws IOException {

        browser.getEngine().load(event.getHomeUrl().toExternalForm());
        backToHomePage = 1;

    }
```
###### \src\main\java\seedu\address\ui\BrowserPanel.java
``` java


}
```
###### \src\main\java\seedu\address\ui\MainWindow.java
``` java
        StatusBarFooter statusBarFooter = new StatusBarFooter(prefs.getAddressBookFilePath(), filteredPersonList);
```
###### \src\main\java\seedu\address\ui\MainWindow.java
``` java

        statusbarPlaceholder.getChildren().add(statusBarFooter.getRoot());

        CommandBox commandBox = new CommandBox(logic);
        commandBoxPlaceholder.getChildren().add(commandBox.getRoot());

    }

```
###### \src\main\java\seedu\address\ui\MainWindow.java
``` java
    /**
     * Changes the theme color to dark of the program
     */
    @FXML
    private void handleDarkTheme() {

        int size = scene.getRoot().getStylesheets().size();

        for (int i = 0; i < size; i++) {
            scene.getRoot().getStylesheets().remove(0);
        }

        scene.getRoot().getStylesheets().add("view/DarkTheme.css");
        scene.getRoot().getStylesheets().add("view/Extensions.css");

    }

    /**
     * Changes the theme color to light of the program
     */
    @FXML
    private void handleLightTheme() {

        int size = scene.getRoot().getStylesheets().size();
        for (int i = 0; i < size; i++) {

            scene.getRoot().getStylesheets().remove(0);

        }
        scene.getRoot().getStylesheets().add("view/LightTheme.css");

    }
```
###### \src\main\java\seedu\address\ui\MainWindow.java
``` java

    public PersonListPanel getPersonListPanel() {
        return this.personListPanel;
    }

    void releaseResources() {
        browserPanel.freeResources();
    }

    @Subscribe
    private void handleShowHelpEvent(ShowHelpRequestEvent event) {
        logger.info(LogsCenter.getEventHandlingLogMessage(event));
        handleHelp();
    }
}
```
###### \src\main\java\seedu\address\ui\PersonCard.java
``` java
    private static String[] colors = { "#ff8080", "#009999", "#4da6ff", "#ff9933", "#00e68a", "#ff80ff", "grey" };
    private static HashMap<String, String> colorMapping = new HashMap<String, String>();
```
###### \src\main\java\seedu\address\ui\PersonCard.java
``` java

    public final ReadOnlyPerson person;

    private final int cardNum;
    private final Logic logic;
    private final Logger logger = LogsCenter.getLogger(CommandBox.class);

    /**
     * Note: Certain keywords such as "location" and "resources" are reserved keywords in JavaFX.
     * As a consequence, UI elements' variable names cannot be set to such keywords
     * or an exception will be thrown by JavaFX during runtime.
     *
     * @see <a href="https://github.com/se-edu/addressbook-level4/issues/336">The issue on AddressBook level 4</a>
     */

    @FXML
    private HBox cardPane;
    @FXML
    private Label name;
    @FXML
    private Button delete;
    @FXML
    private Label id;
    @FXML
    private Label phone;
```
###### \src\main\java\seedu\address\ui\StatusBarFooter.java
``` java
    public static final String SYNC_PERSONLIST_UPADTED_SIZE = "Total size: %d, ";
    public static final String SYNC_STATUS_UPDATED = "Last Updated: %s";
```
###### \src\main\java\seedu\address\ui\StatusBarFooter.java
``` java

    /**
     * Used to generate time stamps.
     *
     * TODO: change clock to an instance variable.
     * We leave it as a static variable because manual dependency injection
     * will require passing down the clock reference all the way from MainApp,
     * but it should be easier once we have factories/DI frameworks.
     */
    private static Clock clock = Clock.systemDefaultZone();

    private static final Logger logger = LogsCenter.getLogger(StatusBarFooter.class);

    private static final String FXML = "StatusBarFooter.fxml";

```
###### \src\main\java\seedu\address\ui\StatusBarFooter.java
``` java
    private ObservableList<ReadOnlyPerson> filteredPersonList;
```
###### \src\main\java\seedu\address\ui\StatusBarFooter.java
``` java

    @FXML
    private StatusBar syncStatus;
    @FXML
    private StatusBar saveLocationStatus;

    public StatusBarFooter(String saveLocation) {
        super(FXML);
        setSyncStatus(SYNC_STATUS_INITIAL);
        setSaveLocation("./" + saveLocation);
        registerAsAnEventHandler(this);
    }

```
###### \src\main\java\seedu\address\ui\StatusBarFooter.java
``` java
    public StatusBarFooter(String saveLocation, ObservableList<ReadOnlyPerson> filteredPersonList) {
        super(FXML);
        this.filteredPersonList = filteredPersonList;
        setSyncStatus(SYNC_STATUS_INITIAL);
        setSaveLocation("./" + saveLocation);
        registerAsAnEventHandler(this);
    }
```
###### \src\main\java\seedu\address\ui\StatusBarFooter.java
``` java

    /**
     * Sets the clock used to determine the current time.
     */
    public static void setClock(Clock clock) {
        StatusBarFooter.clock = clock;
    }

    /**
     * Returns the clock currently in use.
     */
    public static Clock getClock() {
        return clock;
    }

    private void setSaveLocation(String location) {
        Platform.runLater(() -> this.saveLocationStatus.setText(location));
    }

    private void setSyncStatus(String status) {
        Platform.runLater(() -> this.syncStatus.setText(status));
    }

    @Subscribe
    public void handleAddressBookChangedEvent(AddressBookChangedEvent abce) {
        long now = clock.millis();
        String lastUpdated = new Date(now).toString();
        logger.info(LogsCenter.getEventHandlingLogMessage(abce,
                "Setting last updated status to " + lastUpdated));
        setSyncStatus(String.format(SYNC_PERSONLIST_UPADTED_SIZE, filteredPersonList.size())
                + String.format(SYNC_STATUS_UPDATED, lastUpdated));
    }

}
```
###### \src\main\resources\view\default.html
``` html
<html>
<title>Home Page</title>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no">
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.2/css/bootstrap.min.css" integrity="sha384-PsH8R72JQ3SOdhVi3uxftmaW6Vc51MKb0q5P2rRUpPvrszuE4W1povHYgTpBfshb" crossorigin="anonymous">

<style type="text/css">
    html {
        height: 100%;
        width: 100%;
    }

    body {
        height: 100%;
        width: 100%;
        margin: 0px;
        padding: 0px
    }

    img {
        user-drag: none;
        user-select: none;
        -moz-user-select: none;
        -webkit-user-drag: none;
        -webkit-user-select: none;
        -ms-user-select: none;
    }

    strong {
        font-size: 18px;
    }
    p {
        word-break: break-all;
    }

    .container{
        margin: 0px;
        padding: 0px;
        height: 100%;
    }
    .row{
        margin: 0px;
        padding: 0px;
        height: 100%;
    }
</style>

<body>

<!-- First Grid: Picture & Contact Info -->
<div class="row">
    <div class="card col-4">
        <img class="card-img-top" src="../images/bg.jpeg" alt="Card image cap">
        <div class="card-body">

            <strong>
                <h3>Project Name: Unibook</h3>
                <h3>Current Version: <span class='badge badge-warning'>v1.4</span></h3>
                <p>License: <span class='badge badge-info'>MIT</span> Build: <span class='badge badge-success'>passing</span> codacy: <span class='badge badge-primary'>A</span></p>
                <p>UI Design: Linus, Vos</p>
                <p>Function implement: Sirisha, Henning</p>
                <p>Tutorial: T13-B2</p>
                <p>Last updated: 2017/11/02</p>
            </strong>

        </div>
    </div>

    <div class="jumbotron jumbotron-fluid col-8" style="padding: 20px; background: #f7f7f7">
        <h1 style="text-align: center"><b>Unibook Commands</b></h1>

        <div class="card border-primary mb-3">
            <div class="card-header">Home command</div>
            <div class="card-body text-primary">
                <h4 class="card-title">Goes back to the home panel. </h4>
            </div>
        </div>

        <div class="card border-success mb-3">
            <div class="card-header">Add command</div>
            <div class="card-body text-success">
                <h4 class="card-title">Adds a person to the address book. </h4>
                <p class="card-text">Parameters: n/NAME p/PHONE e/EMAIL a/ADDRESS [s/SCORE] [t/TAG]...</p>
            </div>
        </div>
        <div class="card border-secondary mb-3">
            <div class="card-header">Delete command</div>
            <div class="card-body text-secondary">
                <h4 class="card-title">Deletes the person identified by the index number used in the last person listing.</h4>
                <p class="card-text">Parameters: INDEX (must be a positive integer)</p>
            </div>
        </div>

        <div class="card border-success mb-3">
            <div class="card-header">Find command</div>
            <div class="card-body text-success">
                <h4 class="card-title">Finds persons whose names contain any of the given keywords.</h4>
                <p class="card-text">Parameters: find KEYWORD [MORE_KEYWORDS]...</p>
            </div>
        </div>
        <div class="card border-danger mb-3">
            <div class="card-header">Clear command</div>
            <div class="card-body text-danger">
                <h4 class="card-title">Clears all entries from the address book.</h4>
            </div>
        </div>
        <div class="card border-warning mb-3">
            <div class="card-header">Undo command</div>
            <div class="card-body text-warning">
                <h4 class="card-title">Restores the address book to the state before the previous undoable command was executed.</h4>
            </div>
        </div>
        <div class="card border-secondary mb-3">
            <div class="card-header">Redo command</div>
            <div class="card-body text-info">
                <h4 class="card-title">Reverses the most recent undo command.</h4>
            </div>
        </div>

    </div>

</div>
</body>
</html>
```
###### \src\main\resources\view\LightTheme.css
``` css
.root {
    -fx-accent: derive(#f7f5f4, -10%);
    -fx-focus-color: derive(#f7f5f4, -10%);
}

.background {
    -fx-background-color: #f7f7f7;
    background-color: #f7f7f7; /* Used in the default.html file */
}

.v-box {
    -fx-background-color:  #f7f7f7;
}

.label {
    -fx-font-size: 11pt;
    -fx-font-family: "Segoe UI Semibold";
    -fx-text-fill: #000000;
    -fx-opacity: 0.9;
}

.label-bright {
    -fx-font-size: 11pt;
    -fx-font-family: "Segoe UI Semibold";
    -fx-text-fill: gray;
    -fx-opacity: 1;
}

.label-header {
    -fx-font-size: 32pt;
    -fx-font-family: "Segoe UI Light";
    -fx-text-fill: gray;
    -fx-opacity: 1;
}

.text-field {
    -fx-font-size: 12pt;
    -fx-font-family: "Segoe UI Semibold";
}

.tab-pane {
    -fx-padding: 0 0 0 1;
}

.tab-pane .tab-header-area {
    -fx-padding: 0 0 0 0;
    -fx-min-height: 0;
    -fx-max-height: 0;
}

.table-view {
    -fx-base: #f7f7f7;
    -fx-control-inner-background:  #f7f7f7;
    -fx-background-color: #f7f7f7;
    -fx-table-cell-border-color: transparent;
    -fx-table-header-border-color: transparent;
    -fx-padding: 5;
}

.table-view .column-header-background {
    -fx-background-color: transparent;
}

.table-view .column-header, .table-view .filler {
    -fx-size: 35;
    -fx-border-width: 0 0 1 0;
    -fx-background-color: transparent;
    -fx-border-color:
        transparent
        transparent
        derive(-fx-base, 80%)
        transparent;
    -fx-border-insets: 0 10 1 0;
}

.table-view .column-header .label {
    -fx-font-size: 20pt;
    -fx-font-family: "Segoe UI Light";
    -fx-text-fill: gray;
    -fx-alignment: center-left;
    -fx-opacity: 1;
}

.table-view:focused .table-row-cell:filled:focused:selected {
    -fx-background-color: -fx-focus-color;
}

.split-pane:horizontal .split-pane-divider {
    -fx-background-color: transparent;
    -fx-border-color: transparent;
}

.split-pane {
    -fx-border-radius: 1;
    -fx-border-width: 1;
    -fx-background-color: transparent;
}

.list-view {
    -fx-background-insets: 0;
    -fx-padding: 0;
}

.list-cell {
    -fx-label-padding: 0 0 0 0;
    -fx-graphic-text-gap : 0;
    -fx-padding: 0 0 0 0;
}

.list-cell:filled:even {
    -fx-background-color: #ffffff;
}

.list-cell:filled:odd {
    -fx-background-color: #ffffff;
}

.list-cell:filled:selected {
    -fx-background-color: derive(#f7f5f4, -5%);
}

.list-cell:filled:selected #cardPane {
    -fx-border-color: transparent;
    -fx-border-width: 1;
}

.cell_big_label {
    -fx-font-family: "Segoe UI Semibold";
    -fx-font-size: 16px;
    -fx-text-fill: #444344;
}

.cell_id_label {
    -fx-font-family: "Segoe UI Semibold";
    -fx-text-fill: derive(gray, 35%);
    -fx-font-size: 15px;
}

.person_big_label {
    -fx-font-family: "Segoe UI Semibold";
    -fx-font-size: 26px;
    -fx-text-fill: #444344;
}

.person_small_label {
    -fx-font-family: "Lucida Grande", "Segoe UI", Optima;
    -fx-font-size: 15px;
    -fx-text-fill: #848484;
}

.anchor-pane {
     -fx-background-color: transparent;
}

.pane-with-border {
     -fx-background-color: transparent;
     -fx-border-top-width: 1px;
}

.result-pane {
     -fx-background-color: #ffffff;
     -fx-effect: dropshadow(gaussian, derive(#f7f5f4, -15%), 10, 0, 2, 2);
}

.person-detail-panel {
    -fx-background-color: #ffffff;
    -fx-effect: dropshadow(gaussian, derive(#f7f5f4, -15%), 10, 0, 2, 2);
}

.person-vbox {
    -fx-effect: dropshadow(gaussian, derive(#f7f5f4, -15%), 10, 0, -2, 2);
}

.status-bar {
    -fx-background-color: derive(#f7f5f4, 80%);
    -fx-padding: 0 10 0 10;
}

.result-display {
    -fx-background-color: transparent;
    -fx-font-family: "Segoe UI Light";
    -fx-font-size: 12pt;
    -fx-text-fill: gray;
}

.status-bar .label {
    -fx-font-family: "Segoe UI Light";
    -fx-text-fill: derive(#716f70, -10%);
    -fx-font-size: 13px;
}

.status-bar-with-border {
    -fx-background-color: derive(#f7f5f4, 30%);
    -fx-border-color: derive(#f7f5f4, 25%);
    -fx-border-width: 1px;
}

.status-bar-with-border .label {
    -fx-text-fill: gray;
}

.grid-pane {
    -fx-background-color: derive(#f7f5f4, 30%);
    -fx-border-color: derive(#f7f5f4, 30%);
    -fx-border-width: 1px;
}

.grid-pane .anchor-pane {
    -fx-background-color: derive(#f7f5f4, 80%);
}

.context-menu {
    -fx-background-color: derive(#f7f5f4, 50%);
}

.context-menu .label {
    -fx-text-fill: gray;
}

.menu-bar {
    -fx-background-color: derive(#f7f5f4, 80%);
}

.menu-bar .label {
    -fx-font-size: 12pt;
    -fx-font-family: "Segoe UI Light";
    -fx-text-fill: derive(#716f70, -10%);
    -fx-opacity: 0.9;
}

.menu .left-container {
    -fx-background-color: black;
}

/*
 * Metro style Push Button
 * Author: Pedro Duque Vieira
 * http://pixelduke.wordpress.com/2012/10/23/jmetro-windows-8-controls-on-java/
 */
.button {
    -fx-padding: 5 22 5 22;
    -fx-border-color: #e2e2e2;
    -fx-border-width: 2;
    -fx-background-radius: 0;
    -fx-background-color: #f7f5f4;
    -fx-font-family: "Segoe UI", Optima, Helvetica, Arial, sans-serif;
    -fx-font-size: 11pt;
    -fx-text-fill: #d8d8d8;
    -fx-background-insets: 0 0 0 0, 0, 1, 2;
}

.button:hover {
    -fx-background-color: #3a3a3a;
}

.button:pressed, .button:default:hover:pressed {
  -fx-background-color: gray;
  -fx-text-fill: #f7f5f4;
}

.button:focused {
    -fx-border-color: gray, gray;
    -fx-border-width: 1, 1;
    -fx-border-style: solid, segments(1, 1);
    -fx-border-radius: 0, 0;
    -fx-border-insets: 1 1 1 1, 0;
}

.button:disabled, .button:default:disabled {
    -fx-opacity: 0.4;
    -fx-background-color: #f7f5f4;
    -fx-text-fill: gray;
}

.button:default {
    -fx-background-color: -fx-focus-color;
    -fx-text-fill: slategrey;
}

.button:default:hover {
    -fx-background-color: derive(-fx-focus-color, 30%);
}

.dialog-pane {
    -fx-background-color: #f7f5f4;
}

.dialog-pane > *.button-bar > *.container {
    -fx-background-color: #f7f5f4;
}

.dialog-pane > *.label.content {
    -fx-font-size: 14px;
    -fx-font-weight: bold;
    -fx-text-fill: gray;
}

.dialog-pane:header *.header-panel {
    -fx-background-color: derive(#f7f5f4, 25%);
}

.dialog-pane:header *.header-panel *.label {
    -fx-font-size: 18px;
    -fx-font-style: italic;
    -fx-fill: gray;
    -fx-text-fill: gray;
}

.scroll-bar {
    -fx-background-color: derive(#f7f5f4, -5%);
}

.scroll-bar .thumb {
    -fx-background-color: derive(#f7f5f4, -25%);
    -fx-background-insets: 1;
    -fx-background-radius: 18 18 18 18;
}

.scroll-bar .increment-button, .scroll-bar .decrement-button {
    -fx-background-color: transparent;
    -fx-padding: 0 0 0 0;
}

.scroll-bar .increment-arrow, .scroll-bar .decrement-arrow {
    -fx-shape: " ";
}

.scroll-bar:vertical .increment-arrow, .scroll-bar:vertical .decrement-arrow {
    -fx-padding: 5 3 5 3;
}

.scroll-bar:horizontal .increment-arrow, .scroll-bar:horizontal .decrement-arrow {
    -fx-padding: 3 5 3 5;
}

#cardPane {
    -fx-background-color: transparent;
    -fx-border-width: 0;
}
/*
#avatarImage {
    -fx-image: url("../images/avatarGray.png");
}
*/
#phone {
    -fx-image: url("../images/phone.png");
}

#initial_small {
    -fx-font-family: "Roboto";
    -fx-text-fill: #ffffff;
    -fx-font-size: 25px;
}

#initial_big {
    -fx-font-family: "Roboto";
    -fx-text-fill: #ffffff;
    -fx-font-size: 45px;
}

#commandTypeLabel {
    -fx-font-size: 11px;
    -fx-text-fill: #f70d1a;
}

#commandTextField {
    -fx-background-color: transparent;
    -fx-background-insets: 0;
    -fx-border-insets: 0;
    -fx-border-width: 1;
    -fx-font-family: "Segoe UI Light";
    -fx-font-size: 13pt;
    -fx-text-fill: gray;
}

.command-pane {
    -fx-background-color: #ffffff;
    -fx-background-radius: 18 18 18 18;
    -fx-effect: dropshadow(gaussian, derive(#f7f5f4, -15%), 10, 0, 1, 2);
}

#filterField, #personListPanel {
    -fx-effect: innershadow(gaussian, black, 10, 0, 0, 0);
}

#resultDisplay .content {
    -fx-background-color: transparent, #ffffff, transparent, #ffffff;
    -fx-background-radius: 0;
}

#tags {
    -fx-hgap: 7;
    -fx-vgap: 3;
}

#tags .label {
    -fx-font-family: "Segoe UI", Optima;
    -fx-text-fill: white;
    -fx-padding: 1 0 1 0;
    -fx-font-size: 14px;
}
```
###### \src\main\resources\view\StatusBarFooter.fxml
``` fxml
        <?import org.controlsfx.control.StatusBar?>
        <?import javafx.scene.layout.ColumnConstraints?>
        <?import javafx.scene.layout.GridPane?>

<GridPane styleClass="grid-pane" xmlns="http://javafx.com/javafx/8" xmlns:fx="http://javafx.com/fxml/1">
<columnConstraints>
  <ColumnConstraints hgrow="SOMETIMES" minWidth="10" prefWidth="100" />
  <ColumnConstraints hgrow="SOMETIMES" minWidth="10" prefWidth="100" />
</columnConstraints>
<StatusBar styleClass="anchor-pane" fx:id="syncStatus" />
<StatusBar styleClass="anchor-pane" fx:id="saveLocationStatus" GridPane.columnIndex="1" nodeOrientation="RIGHT_TO_LEFT" />
</GridPane>
```
###### \src\main\resources\view\StatusBarFooter.fxml
``` fxml

```
###### \src\test\java\seedu\address\logic\commands\HomeCommandTest.java
``` java
package seedu.address.logic.commands;

import static seedu.address.logic.commands.CommandTestUtil.assertCommandSuccess;
import static seedu.address.logic.commands.CommandTestUtil.showFirstPersonOnly;
import static seedu.address.testutil.TypicalPersons.getTypicalAddressBook;

import org.junit.Before;
import org.junit.Test;

import seedu.address.logic.CommandHistory;
import seedu.address.logic.UndoRedoStack;
import seedu.address.model.Model;
import seedu.address.model.ModelManager;
import seedu.address.model.UserPrefs;

public class HomeCommandTest {

    private Model model;
    private Model expectedModel;
    private HomeCommand homeCommand;

    @Before
    public void setUp() {
        model = new ModelManager(getTypicalAddressBook(), new UserPrefs());
        expectedModel = new ModelManager(model.getAddressBook(), new UserPrefs());

        homeCommand = new HomeCommand();
        homeCommand.setData(model, new CommandHistory(), new UndoRedoStack());
    }

    @Test
    public void execute_listIsNotFiltered_showsSameList() {
        assertCommandSuccess(homeCommand, model, HomeCommand.MESSAGE_SUCCESS, expectedModel);
    }

    @Test
    public void execute_listIsFiltered_showsEverything() {
        showFirstPersonOnly(model);
        assertCommandSuccess(homeCommand, model, HomeCommand.MESSAGE_SUCCESS, expectedModel);
    }
}

```
###### \src\test\java\seedu\address\logic\commands\HomeCommandTest.java
``` java

```
###### \src\test\java\systemtests\AddressBookSystemTest.java
``` java
        assertEquals(expectedSyncStatus, handle.getSyncStatus().split(", ")[1]);
```
###### \src\test\java\systemtests\AddressBookSystemTest.java
``` java
        assertFalse(handle.isSaveLocationChanged());
    }

    /**
     * Asserts that the starting state of the application is correct.
     */
    private void assertApplicationStartingStateIsCorrect() {
        try {
            assertEquals("", getCommandBox().getInput());
            assertEquals("", getResultDisplay().getText());
            assertListMatching(getPersonListPanel(), getModel().getFilteredPersonList());
            assertEquals(MainApp.class.getResource(FXML_FILE_FOLDER + DEFAULT_PAGE),
                    getBrowserPanel().getLoadedUrl());
            assertEquals("./" + testApp.getStorageSaveLocation(), getStatusBarFooter().getSaveLocation());
            assertEquals(SYNC_STATUS_INITIAL, getStatusBarFooter().getSyncStatus());
        } catch (Exception e) {
            throw new AssertionError("Starting state is wrong.", e);
        }
    }

    /**
     * Returns a defensive copy of the current model.
     */
    protected Model getModel() {
        return testApp.getModel();
    }
}
```
###### \src\test\java\systemtests\ClearCommandSystemTest.java
``` java
        assertStatusBarUnchangedExceptSyncStatus();
```
###### \src\test\java\systemtests\ClearCommandSystemTest.java
``` java

    }
}
```
