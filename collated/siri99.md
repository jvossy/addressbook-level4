# siri99
###### \src\main\java\seedu\address\commons\util\StringUtil.java
``` java
    /**
     * Returns true if the {@code sentence} contains any part of the {@code word}.
     *   Ignores case, and full word match is not required, word just has to be a substring.
     *   <br>examples:<pre>
     *       containsSubstringOfWord("ABc def", "abc") == true
     *       containsSubstringOfWord("ABc def", "DEF") == true
     *       containsSubstringOfWord("ABc def", "AB") == false //not a full word match
     *       </pre>
     * @param sentence cannot be null
     * @param word cannot be null, cannot be empty, must be a single word with minimum 2 characters
     */
    public static boolean containsSubstringOfWord(String sentence, String word) {
        requireNonNull(sentence);
        requireNonNull(word);

        String preppedWord = word.trim();
        checkArgument(!preppedWord.isEmpty(), "Word parameter cannot be empty");
        checkArgument(preppedWord.split("\\s+").length == 1, "Word parameter should be a single word");

        String preppedSentence = sentence;
        String[] wordsInPreppedSentence = preppedSentence.split("\\s+");

        if (preppedWord.length() >= 2) {
            for (String wordInSentence : wordsInPreppedSentence) {
                if (wordInSentence.toLowerCase().contains(preppedWord.toLowerCase())) {
                    return true;
                }
            }
        }
        return false;
    }
```
###### \src\main\java\seedu\address\commons\util\StringUtil.java
``` java

    /**
     * Returns a detailed message of the t, including the stack trace.
     */
    public static String getDetails(Throwable t) {
        requireNonNull(t);
        StringWriter sw = new StringWriter();
        t.printStackTrace(new PrintWriter(sw));
        return t.getMessage() + "\n" + sw.toString();
    }

    /**
     * Returns true if {@code s} represents a non-zero unsigned integer
     * e.g. 1, 2, 3, ..., {@code Integer.MAX_VALUE} <br>
     * Will return false for any other non-null string input
     * e.g. empty string, "-1", "0", "+1", and " 2 " (untrimmed), "3 0" (contains whitespace), "1 a" (contains letters)
     * @throws NullPointerException if {@code s} is null.
     */
    public static boolean isNonZeroUnsignedInteger(String s) {
        requireNonNull(s);

        try {
            int value = Integer.parseInt(s);
            return value > 0 && !s.startsWith("+"); // "+1" is successfully parsed by Integer#parseInt(String)
        } catch (NumberFormatException nfe) {
            return false;
        }
    }
}
```
###### \src\main\java\seedu\address\logic\commands\EditCommand.java
``` java
        Birthday updatedBirthday = editPersonDescriptor.getBirthday().orElse(personToEdit.getBirthday());
```
###### \src\main\java\seedu\address\logic\commands\EditCommand.java
``` java
        Email updatedEmail = editPersonDescriptor.getEmail().orElse(personToEdit.getEmail());
        Address updatedAddress = editPersonDescriptor.getAddress().orElse(personToEdit.getAddress());
        Set<Tag> updatedTags = editPersonDescriptor.getTags().orElse(personToEdit.getTags());
        Score updatedScore = editPersonDescriptor.getScore().orElse(personToEdit.getScore());
        return new Person(updatedName, updatedPhone, updatedBirthday, updatedEmail, updatedAddress,
                updatedScore, updatedTags);
    }

    @Override
    public boolean equals(Object other) {
        // short circuit if same object
        if (other == this) {
            return true;
        }

        // instanceof handles nulls
        if (!(other instanceof EditCommand)) {
            return false;
        }

        // state check
        EditCommand e = (EditCommand) other;
        return index.equals(e.index)
                && editPersonDescriptor.equals(e.editPersonDescriptor);
    }

    /**
     * Stores the details to edit the person with. Each non-empty field value will replace the
     * corresponding field value of the person.
     * Also, travis is bugged, so am adding code to force another commit.
     */
    public static class EditPersonDescriptor {
        private Name name;
        private Phone phone;
        private Birthday birthday;
        private Email email;
        private Address address;
        private Score score;
        private Set<Tag> tags;

        public EditPersonDescriptor() {}

        public EditPersonDescriptor(EditPersonDescriptor toCopy) {
            this.name = toCopy.name;
            this.phone = toCopy.phone;
            this.birthday = toCopy.birthday;
            this.email = toCopy.email;
            this.address = toCopy.address;
            this.score = toCopy.score;
            this.tags = toCopy.tags;
        }

        /**
         * Returns true if at least one field is edited.
         */
        public boolean isAnyFieldEdited() {
            return CollectionUtil.isAnyNonNull(this.name, this.phone, this.birthday, this.email,
                    this.address, this.score, this.tags);
        }

        public void setName(Name name) {
            this.name = name;
        }

        public Optional<Name> getName() {
            return Optional.ofNullable(name);
        }

        public void setPhone(Phone phone) {
            this.phone = phone;
        }

        public Optional<Phone> getPhone() {
            return Optional.ofNullable(phone);
        }

```
###### \src\main\java\seedu\address\logic\commands\EditCommand.java
``` java
        public void setBirthday(Birthday birthday) {
            if (!(birthday.toString().equals("No Birthday Listed"))) {
                this.birthday = birthday;
            }
        }

        public Optional<Birthday> getBirthday() {
            return Optional.ofNullable(birthday);
        }
```
###### \src\main\java\seedu\address\logic\commands\EditCommand.java
``` java

        public void setEmail(Email email) {
            this.email = email;
        }

        public Optional<Email> getEmail() {
            return Optional.ofNullable(email);
        }

        public void setAddress(Address address) {
            this.address = address;
        }

        public Optional<Address> getAddress() {
            return Optional.ofNullable(address);
        }

        public void setTags(Set<Tag> tags) {
            this.tags = tags;
        }

        public void setScore(Score score) {
            if (score.toString().equals("")) {
                return;
            } else {
                this.score = score;
            }
        }

        public Optional<Score> getScore() {
            return Optional.ofNullable(score);
        }

        public Optional<Set<Tag>> getTags() {
            return Optional.ofNullable(tags);
        }

        @Override
        public boolean equals(Object other) {
            // short circuit if same object
            if (other == this) {
                return true;
            }

            // instanceof handles nulls
            if (!(other instanceof EditPersonDescriptor)) {
                return false;
            }

            // state check
            EditPersonDescriptor e = (EditPersonDescriptor) other;

            return getName().equals(e.getName())
                    && getPhone().equals(e.getPhone())
                    && getBirthday().equals(e.getBirthday())
                    && getEmail().equals(e.getEmail())
                    && getAddress().equals(e.getAddress())
                    && getScore().equals(e.getScore())
                    && getTags().equals(e.getTags());
        }
    }
}
```
###### \src\main\java\seedu\address\logic\commands\FavCommand.java
``` java
package seedu.address.logic.commands;

import java.util.List;

import seedu.address.commons.core.Messages;
import seedu.address.commons.core.index.Index;
import seedu.address.logic.commands.exceptions.CommandException;
import seedu.address.model.person.ReadOnlyPerson;
import seedu.address.model.person.exceptions.DuplicatePersonException;

/**
 * Adds a person identified using the index into the Favourite list.
 */
public class FavCommand extends UndoableCommand {
    public static final String COMMAND_WORD = "fav";
    public static final String COMMAND_WORD_ALIAS = "fv";

    public static final String MESSAGE_USAGE = COMMAND_WORD
            + ": Add a person identified by the index number used to the Favourite list.\n"
            + "Parameters: INDEX (must be a positive integer)\n"
            + "Example: " + COMMAND_WORD + " 1";

    public static final String MESSAGE_FAV_PERSON_SUCCESS = "Added person to Favourite list: %1$s";

    private final Index targetIndex;

    public FavCommand(Index targetIndex) {
        this.targetIndex = targetIndex;
    }

    @Override
    public CommandResult executeUndoableCommand() throws CommandException {

        List<ReadOnlyPerson> lastShownList = model.getFilteredPersonList();

        if (targetIndex.getZeroBased() >= lastShownList.size()) {
            throw new CommandException(Messages.MESSAGE_INVALID_PERSON_DISPLAYED_INDEX);
        }

        ReadOnlyPerson personToFav = lastShownList.get(targetIndex.getZeroBased());
        try {
            model.addFavouritePerson(personToFav);
        } catch (DuplicatePersonException e) {
            assert false : "The target person is already in the favourite list";
        }

        return new CommandResult(String.format(MESSAGE_FAV_PERSON_SUCCESS, personToFav));
    }

    @Override
    public boolean equals(Object other) {
        return other == this // short circuit if same object
                || (other instanceof FavCommand // instanceof handles nulls
                && this.targetIndex.equals(((FavCommand) other).targetIndex)); // state check
    }
}
```
###### \src\main\java\seedu\address\logic\commands\FavCommand.java
``` java

```
###### \src\main\java\seedu\address\logic\commands\FavouriteListCommand.java
``` java
package seedu.address.logic.commands;

import static seedu.address.model.Model.PREDICATE_SHOW_ALL_FAVOURITE_PERSONS;

/**
 * Displays the Favourite list.
 */

public class FavouriteListCommand extends UndoableCommand {

    public static final String COMMAND_WORD = "favlist";
    public static final String COMMAND_WORD_ALIAS = "fl";

    public static final String MESSAGE_SUCCESS = "Listed all favourite contacts";

    @Override
    public CommandResult executeUndoableCommand() {
        model.changeListTo(COMMAND_WORD);
        model.updateFilteredFavouritePersonList(PREDICATE_SHOW_ALL_FAVOURITE_PERSONS);
        return new CommandResult(MESSAGE_SUCCESS);
    }
}
```
###### \src\main\java\seedu\address\logic\commands\FavouriteListCommand.java
``` java

```
###### \src\main\java\seedu\address\logic\commands\SortCommand.java
``` java
package seedu.address.logic.commands;

import seedu.address.logic.commands.exceptions.CommandException;

/**
* Sorts all persons in the address book by indicated format.
*/
public class SortCommand extends Command {

    public static final String COMMAND_WORD = "sort";
    public static final String COMMAND_WORD_ALIAS = "so";

    public static final String MESSAGE_USAGE = COMMAND_WORD + ": Sorts the address book in selected format.\n"
            + "Example: " + COMMAND_WORD + " : default sorts in alphabhetical order\n"
            + "Example: " + COMMAND_WORD + " name : sorts in alphabhetical order \n"
            + "Example: " + COMMAND_WORD + " birthday or " + COMMAND_WORD + " b : sorts in ascending order"
            + " of birthdays";

    public static final String MESSAGE_SUCCESS_NAME = "Sorted successfully by Name, Listing all persons below";

    public static final String MESSAGE_SUCCESS_BIRTHDAY = "Sorted successfully by Birthdays, Listing all persons below";

    private String sortFilter;

    public SortCommand (String sortFilter) {
        //Null sort Filter refers to default sort command i.e. sort by name
        this.sortFilter = sortFilter;
    }

    @Override
    public CommandResult execute() throws CommandException {
        switch(sortFilter) {
        case "name":
        default:
            model.sortFilteredPersonListName();
            return new CommandResult(MESSAGE_SUCCESS_NAME);

        case "birthday":
        case "b":
            model.sortFilteredPersonListBirthday();
            return new CommandResult(MESSAGE_SUCCESS_BIRTHDAY);
        }
    }

    @Override
    public boolean equals(Object other) {
        // short circuit if same object
        if (other == this) {
            return true;
        }

        // if not the same object, return false
        if (!(other instanceof SortCommand)) {
            return false;
        }

        SortCommand s = (SortCommand) other;
        return sortFilter.equals(s.sortFilter);
    }
}
```
###### \src\main\java\seedu\address\logic\commands\SortCommand.java
``` java

```
###### \src\main\java\seedu\address\logic\commands\UnfavCommand.java
``` java
package seedu.address.logic.commands;

import java.util.List;

import seedu.address.commons.core.Messages;
import seedu.address.commons.core.index.Index;
import seedu.address.logic.commands.exceptions.CommandException;
import seedu.address.model.person.ReadOnlyPerson;
import seedu.address.model.person.exceptions.PersonNotFoundException;

/**
 * Removes a person identified using it's last displayed index from the favourite list.
 */
public class UnfavCommand extends UndoableCommand {

    public static final String COMMAND_WORD = "unfav";
    public static final String COMMAND_WORD_ALIAS = "unfv";

    public static final String MESSAGE_USAGE = COMMAND_WORD
            + ": Remove a person identified by the index number from the Favourite list.\n"
            + "Parameters: INDEX (must be a positive integer)\n"
            + "Example: " + COMMAND_WORD + " 1";

    public static final String MESSAGE_UNFAV_PERSON_SUCCESS = "Removed person from favourite list: %1$s";

    private final Index targetIndex;

    public UnfavCommand(Index targetIndex) {
        this.targetIndex = targetIndex;
    }

    @Override
    public CommandResult executeUndoableCommand() throws CommandException {

        List<ReadOnlyPerson> lastShownList = model.getFilteredFavouritePersonList();

        if (targetIndex.getZeroBased() >= lastShownList.size()) {
            throw new CommandException(Messages.MESSAGE_INVALID_PERSON_DISPLAYED_INDEX);
        }

        ReadOnlyPerson personToUnfav = lastShownList.get(targetIndex.getZeroBased());

        try {
            model.removeFavouritePerson(personToUnfav);
        } catch (PersonNotFoundException e) {
            assert false : "The selected person is not in favourite list";
        }

        return new CommandResult(String.format(MESSAGE_UNFAV_PERSON_SUCCESS, personToUnfav));
    }

    @Override
    public boolean equals(Object other) {
        return other == this // short circuit if same object
                || (other instanceof UnfavCommand // instanceof handles nulls
                && this.targetIndex.equals(((UnfavCommand) other).targetIndex)); // state check
    }

}
```
###### \src\main\java\seedu\address\logic\commands\UnfavCommand.java
``` java

```
###### \src\main\java\seedu\address\logic\Logic.java
``` java
    /** Returns an unmodifiable view of the filtered list of favourited persons */
    ObservableList<ReadOnlyPerson> getFilteredFavoritePersonList();

    String getCurrentList();
```
###### \src\main\java\seedu\address\logic\Logic.java
``` java

    /** Returns the list of input entered by the user, encapsulated in a {@code ListElementPointer} object */
    ListElementPointer getHistorySnapshot();
}
```
###### \src\main\java\seedu\address\logic\LogicManager.java
``` java
    @Override
    public ObservableList<ReadOnlyPerson> getFilteredFavoritePersonList() {
        return model.getFilteredFavouritePersonList();
    }

    @Override
    public String getCurrentList() {
        return model.getCurrentList();
    }
```
###### \src\main\java\seedu\address\logic\LogicManager.java
``` java

    @Override
    public ListElementPointer getHistorySnapshot() {
        return new ListElementPointer(history.getHistory());
    }
}
```
###### \src\main\java\seedu\address\logic\parser\AddCommandParser.java
``` java
            Birthday birthday = ParserUtil.parseBirthday(argMultimap.getValue(PREFIX_BIRTHDAY)).get();
```
###### \src\main\java\seedu\address\logic\parser\AddCommandParser.java
``` java
            Email email = ParserUtil.parseEmail(argMultimap.getValue(PREFIX_EMAIL)).get();
            Address address = ParserUtil.parseAddress(argMultimap.getValue(PREFIX_ADDRESS)).get();
            Score score = ParserUtil.parseScore(argMultimap.getValue(PREFIX_SCORE)).get();
            Set<Tag> tagList = ParserUtil.parseTags(argMultimap.getAllValues(PREFIX_TAG));

            ReadOnlyPerson person = new Person(name, phone, birthday, email, address, score, tagList);

            return new AddCommand(person);
        } catch (IllegalValueException ive) {
            throw new ParseException(ive.getMessage(), ive);
        }
    }

    /**
     * Returns true if none of the prefixes contains empty {@code Optional} values in the given
     * {@code ArgumentMultimap}.
     */
    private static boolean arePrefixesPresent(ArgumentMultimap argumentMultimap, Prefix... prefixes) {
        return Stream.of(prefixes).allMatch(prefix -> argumentMultimap.getValue(prefix).isPresent());
    }

}
```
###### \src\main\java\seedu\address\logic\parser\AddressBookParser.java
``` java
        case SortCommand.COMMAND_WORD:
        case SortCommand.COMMAND_WORD_ALIAS:
            return new SortCommandParser().parse(arguments);
```
###### \src\main\java\seedu\address\logic\parser\AddressBookParser.java
``` java

        case DeleteCommand.COMMAND_WORD:
        case DeleteCommand.COMMAND_WORD_ALIAS:
            return new DeleteCommandParser().parse(arguments);

        case ClearCommand.COMMAND_WORD:
        case ClearCommand.COMMAND_WORD_ALIAS:
            return new ClearCommand();

```
###### \src\main\java\seedu\address\logic\parser\AddressBookParser.java
``` java
        case FavCommand.COMMAND_WORD:
        case FavCommand.COMMAND_WORD_ALIAS:
            return new FavCommandParser().parse(arguments);

        case UnfavCommand.COMMAND_WORD:
        case UnfavCommand.COMMAND_WORD_ALIAS:
            return new UnfavCommandParser().parse(arguments);
```
###### \src\main\java\seedu\address\logic\parser\AddressBookParser.java
``` java

        case FindCommand.COMMAND_WORD:
        case FindCommand.COMMAND_WORD_ALIAS:
            return new FindCommandParser().parse(arguments);

```
###### \src\main\java\seedu\address\logic\parser\AddressBookParser.java
``` java
        case FavouriteListCommand.COMMAND_WORD:
        case FavouriteListCommand.COMMAND_WORD_ALIAS:
            return new FavouriteListCommand();
```
###### \src\main\java\seedu\address\logic\parser\AddressBookParser.java
``` java

```
###### \src\main\java\seedu\address\logic\parser\EditCommandParser.java
``` java
            ParserUtil.parseBirthday(argMultimap.getValue(PREFIX_BIRTHDAY)).ifPresent
                (editPersonDescriptor::setBirthday);
```
###### \src\main\java\seedu\address\logic\parser\EditCommandParser.java
``` java
            ParserUtil.parseEmail(argMultimap.getValue(PREFIX_EMAIL)).ifPresent(editPersonDescriptor::setEmail);
            ParserUtil.parseAddress(argMultimap.getValue(PREFIX_ADDRESS)).ifPresent(editPersonDescriptor::setAddress);
            ParserUtil.parseScore(argMultimap.getValue(PREFIX_SCORE)).ifPresent(editPersonDescriptor::setScore);
            parseTagsForEdit(argMultimap.getAllValues(PREFIX_TAG)).ifPresent(editPersonDescriptor::setTags);
        } catch (IllegalValueException ive) {
            throw new ParseException(ive.getMessage(), ive);
        }

        if (!editPersonDescriptor.isAnyFieldEdited()) {
            throw new ParseException(EditCommand.MESSAGE_NOT_EDITED);
        }

        return new EditCommand(index, editPersonDescriptor);
    }

    /**
     * Parses {@code Collection<String> tags} into a {@code Set<Tag>} if {@code tags} is non-empty.
     * If {@code tags} contain only one element which is an empty string, it will be parsed into a
     * {@code Set<Tag>} containing zero tags.
     */
    private Optional<Set<Tag>> parseTagsForEdit(Collection<String> tags) throws IllegalValueException {
        assert tags != null;

        if (tags.isEmpty()) {
            return Optional.empty();
        }
        Collection<String> tagSet = tags.size() == 1 && tags.contains("") ? Collections.emptySet() : tags;
        return Optional.of(ParserUtil.parseTags(tagSet));
    }

}
```
###### \src\main\java\seedu\address\logic\parser\FavCommandParser.java
``` java
package seedu.address.logic.parser;

import static seedu.address.commons.core.Messages.MESSAGE_INVALID_COMMAND_FORMAT;

import seedu.address.commons.core.index.Index;
import seedu.address.commons.exceptions.IllegalValueException;
import seedu.address.logic.commands.FavCommand;
import seedu.address.logic.parser.exceptions.ParseException;

/**
 * Parses input arguments and creates a new FavCommand object
 */

public class FavCommandParser implements Parser<FavCommand> {

    /**
     * Parses the given {@code String} of arguments in the context of the FavCommand
     * and returns an FavCommand object for execution.
     *
     * @throws ParseException if the user input does not conform the expected format
     */


    public FavCommand parse(String args) throws ParseException {
        try {
            Index index = ParserUtil.parseIndex(args);
            return new FavCommand(index);
        } catch (IllegalValueException ive) {
            throw new ParseException(
                    String.format(MESSAGE_INVALID_COMMAND_FORMAT, FavCommand.MESSAGE_USAGE));
        }
    }
}
```
###### \src\main\java\seedu\address\logic\parser\FavCommandParser.java
``` java

```
###### \src\main\java\seedu\address\logic\parser\ParserUtil.java
``` java
    /**
     * Parses a {@code Optional<String> birthday} into an {@code Optional<Birthday>} if {@code birthday} is present.
     * See header comment of this class regarding the use of {@code Optional} parameters.
     */
    public static Optional<Birthday> parseBirthday(Optional<String> birthday) throws IllegalValueException {
        requireNonNull(birthday);
        //return birthday.isPresent() ? Optional.of(new Birthday(birthday.get())) : Optional.empty();
        return birthday.isPresent() ? Optional.of(new Birthday(birthday.get())) : Optional.of
                (new Birthday("valueNotFound"));
    }
```
###### \src\main\java\seedu\address\logic\parser\ParserUtil.java
``` java

    /**
     * Parses a {@code Optional<String> address} into an {@code Optional<Address>} if {@code address} is present.
     * See header comment of this class regarding the use of {@code Optional} parameters.
     */
    public static Optional<Address> parseAddress(Optional<String> address) throws IllegalValueException {
        requireNonNull(address);
        return address.isPresent() ? Optional.of(new Address(address.get())) : Optional.empty();
    }

    /**
     * Parses a {@code Optional<String> email} into an {@code Optional<Email>} if {@code email} is present.
     * See header comment of this class regarding the use of {@code Optional} parameters.
     */
    public static Optional<Email> parseEmail(Optional<String> email) throws IllegalValueException {
        requireNonNull(email);
        return email.isPresent() ? Optional.of(new Email(email.get())) : Optional.empty();
    }

    /**
     * Parses a {@code Optional<String> score} into an {@code Optional<Score>} if {@code score} is present.
     * See header comment of this class regarding the use of {@code Optional} parameters.
     */
```
###### \src\main\java\seedu\address\logic\parser\SortCommandParser.java
``` java
package seedu.address.logic.parser;
import static java.util.Objects.requireNonNull;
import static seedu.address.commons.core.Messages.MESSAGE_INVALID_COMMAND_FORMAT;

import seedu.address.logic.commands.SortCommand;
import seedu.address.logic.parser.exceptions.ParseException;

/**
 * Parses input arguments and creates a new SelectCommand object
 */
public class SortCommandParser implements Parser<SortCommand> {
    /**
     * Parses the given {@code String} of arguments in the context of the SortCommand
     * and returns an SortCommand object for execution.
     *
     * @throws ParseException if the user input does not conform the expected format
     */
    public SortCommand parse(String args) throws ParseException {
        requireNonNull(args);
        ArgumentMultimap argMultimap = ArgumentTokenizer.tokenize(args, new Prefix(""));

        String sortFilter;
        sortFilter = argMultimap.getPreamble();

        if (sortFilter.equals("sort")) {
            //No arguments, set to default filter "name" which sorts in alphabhetical order
            sortFilter = "";
        }

        if (!((sortFilter.equals("name") || sortFilter.equals("birthday") || sortFilter.equals("b")
                || sortFilter.equals("")))) {
            throw new ParseException(String.format(MESSAGE_INVALID_COMMAND_FORMAT, SortCommand.MESSAGE_USAGE));
        }
        return new SortCommand(sortFilter);
    }
}
```
###### \src\main\java\seedu\address\logic\parser\SortCommandParser.java
``` java

```
###### \src\main\java\seedu\address\logic\parser\UnfavCommandParser.java
``` java
package seedu.address.logic.parser;

import static seedu.address.commons.core.Messages.MESSAGE_INVALID_COMMAND_FORMAT;

import seedu.address.commons.core.index.Index;
import seedu.address.commons.exceptions.IllegalValueException;
import seedu.address.logic.commands.UnfavCommand;
import seedu.address.logic.parser.exceptions.ParseException;


/**
 * Parses input arguments and creates a new UnfavCommand object
 */

public class UnfavCommandParser implements Parser<UnfavCommand> {
    /**
     * Parses the given {@code String} of arguments in the context of the UnfavCommand
     * and returns an UnfavCommand object for execution.
     *
     * @throws ParseException if the user input does not conform the expected format
     */

    public UnfavCommand parse(String args) throws ParseException {

        try {
            Index index = ParserUtil.parseIndex(args);
            return new UnfavCommand(index);
        } catch (IllegalValueException ive) {
            throw new ParseException(
                    String.format(MESSAGE_INVALID_COMMAND_FORMAT, UnfavCommand.MESSAGE_USAGE));
        }
    }
}
```
###### \src\main\java\seedu\address\logic\parser\UnfavCommandParser.java
``` java

```
###### \src\main\java\seedu\address\model\AddressBook.java
``` java
    public void setFavouritePersons(List<? extends ReadOnlyPerson> persons) throws DuplicatePersonException {
        this.favouritePersons.setPersons(persons);
    }
```
###### \src\main\java\seedu\address\model\AddressBook.java
``` java

    public void setTags(Set<Tag> tags) {
        this.tags.setTags(tags);
    }

    /**
     * Resets the existing data of this {@code AddressBook} with {@code newData}.
     */
    public void resetData(ReadOnlyAddressBook newData) {
        requireNonNull(newData);
        try {
            setPersons(newData.getPersonList());
        } catch (DuplicatePersonException e) {
            assert false : "AddressBooks should not have duplicate persons";
        }

```
###### \src\main\java\seedu\address\model\AddressBook.java
``` java
        try {
            setFavouritePersons(newData.getFavouritePersonList());
        } catch (DuplicatePersonException e) {
            assert false : "AddressBooks should not have duplicate persons";
        }
```
###### \src\main\java\seedu\address\model\AddressBook.java
``` java

        setTags(new HashSet<>(newData.getTagList()));
        syncMasterTagListWith(persons);
    }

    //// person-level operations

    /**
     * Adds a person to the address book.
     * Also checks the new person's tags and updates {@link #tags} with any new tags found,
     * and updates the Tag objects in the person to point to those in {@link #tags}.
     *
     * @throws DuplicatePersonException if an equivalent person already exists.
     */
    public void addPerson(ReadOnlyPerson p) throws DuplicatePersonException {
        Person newPerson = new Person(p);
        syncMasterTagListWith(newPerson);
        // TODO: the tags master list will be updated even though the below line fails.
        // This can cause the tags master list to have additional tags that are not tagged to any person
        // in the person list.
        persons.add(newPerson);
    }

```
###### \src\main\java\seedu\address\model\AddressBook.java
``` java
    /** Adds favourite person to addressBook
     * Also updates new tags found (if any)
     */
    public void addFavouritePerson(ReadOnlyPerson p) throws DuplicatePersonException {
        Person newPerson = new Person(p);
        syncMasterTagListWith(newPerson);
        favouritePersons.add(newPerson);
    }
```
###### \src\main\java\seedu\address\model\AddressBook.java
``` java

    /**
     * Replaces the given person {@code target} in the list with {@code editedReadOnlyPerson}.
     * {@code AddressBook}'s tag list will be updated with the tags of {@code editedReadOnlyPerson}.
     *
     * Also replaces the given person {@code target} in the Favourite list with {@code editedReadOnlyPerson}
     * if same person is listed on Favourite list too.
     *
     * @throws DuplicatePersonException if updating the person's details causes the person to be equivalent to
     *                                  another existing person in the list.
     * @throws PersonNotFoundException  if {@code target} could not be found in the list.
     * @see #syncMasterTagListWith(Person)
     */
    public void updatePerson(ReadOnlyPerson target, ReadOnlyPerson editedReadOnlyPerson)
            throws DuplicatePersonException, PersonNotFoundException {
        requireNonNull(editedReadOnlyPerson);

        Person editedPerson = new Person(editedReadOnlyPerson);
        syncMasterTagListWith(editedPerson);
        // TODO: the tags master list will be updated even though the below line fails.
        // This can cause the tags master list to have additional tags that are not tagged to any person
        // in the person list.
        persons.setPerson(target, editedPerson);
        /* Line makes sure that Favourite List is synced with main list, if a person is
         * edited from the main list and is also present on the Favourite List,
         * the person will be automatically edited from fav list too
         */
        if (favouritePersons.contains(target)) {
            favouritePersons.setPerson(target, editedPerson);
        }
    }

```
###### \src\main\java\seedu\address\model\AddressBook.java
``` java
    /**
     * Sorts the list of people in the address book.
     */
    public void sortPersonsByName() {
        persons.sortPersonsByName();
    }
```
###### \src\main\java\seedu\address\model\AddressBook.java
``` java

    public void sortPersonsByBirthday() {
        persons.sortPersonsByBirthday();
    }

    /**
     * Ensures that every tag in this person:
     * - exists in the master list {@link #tags}
     * - points to a Tag object in the master list
     */
    private void syncMasterTagListWith(Person person) {
        final UniqueTagList personTags = new UniqueTagList(person.getTags());
        tags.mergeFrom(personTags);

        // Create map with values = tag object references in the master list
        // used for checking person tag references
        final Map<Tag, Tag> masterTagObjects = new HashMap<>();
        tags.forEach(tag -> masterTagObjects.put(tag, tag));

        // Rebuild the list of person tags to point to the relevant tags in the master tag list.
        final Set<Tag> correctTagReferences = new HashSet<>();
        personTags.forEach(tag -> correctTagReferences.add(masterTagObjects.get(tag)));
        person.setTags(correctTagReferences);
    }

    /**
     * Ensures that every tag in these persons:
     * - exists in the master list {@link #tags}
     * - points to a Tag object in the master list
     *
     * @see #syncMasterTagListWith(Person)
     */
    private void syncMasterTagListWith(UniquePersonList persons) {
        persons.forEach(this::syncMasterTagListWith);
    }

    /**
     * Removes {@code key} from this {@code AddressBook}.
     * Also removes {@code key} from the Favourite List if same person is listed on Fav list too.
     * @throws PersonNotFoundException if the {@code key} is not in this {@code AddressBook}.
     */
    public boolean removePerson(ReadOnlyPerson key) throws PersonNotFoundException {

        if (persons.remove(key)) {
            /* Line makes sure that Favourite List is synced with main list, if a person is
             * deleted from the main list and is also present on the Favourite List,
             * the person will be automatically deleted from fav list too
             */
            if (favouritePersons.contains(key)) {
                favouritePersons.remove(key);
            }
            return true; // returns true if Person is in the main list irrespective of Fav list
        } else {
            throw new PersonNotFoundException();
        }
    }

```
###### \src\main\java\seedu\address\model\AddressBook.java
``` java
    /**
     * Removes {@code key} from this {@code AddressBook}.
     * @throws PersonNotFoundException if the {@code key} is not in this {@code AddressBook}.
     */
    public boolean removeFavouritePerson(ReadOnlyPerson key) throws PersonNotFoundException {
        if (favouritePersons.remove(key)) {
            return true;
        } else {
            throw new PersonNotFoundException();
        }
    }
```
###### \src\main\java\seedu\address\model\AddressBook.java
``` java

    //// tag-level operations

    public void addTag(Tag t) throws UniqueTagList.DuplicateTagException {
        tags.add(t);
    }

    //// util methods

    @Override
    public String toString() {
        return persons.asObservableList().size() + " persons, " + favouritePersons.asObservableList().size()
                + " favourite persons, " + tags.asObservableList().size() + " tags";
        // TODO: refine later
    }

    @Override
    public ObservableList<ReadOnlyPerson> getPersonList() {
        return persons.asObservableList();
    }

```
###### \src\main\java\seedu\address\model\AddressBook.java
``` java
    @Override
    public ObservableList<ReadOnlyPerson> getFavouritePersonList() {
        return favouritePersons.asObservableList();
    }
```
###### \src\main\java\seedu\address\model\AddressBook.java
``` java

    @Override
    public ObservableList<Tag> getTagList() {
        return tags.asObservableList();
    }

    @Override
    public boolean equals(Object other) {
        return other == this // short circuit if same object
                || (other instanceof AddressBook // instanceof handles nulls
                && this.persons.equals(((AddressBook) other).persons)
                && this.favouritePersons.equals(((AddressBook) other).favouritePersons)
                && this.tags.equalsOrderInsensitive(((AddressBook) other).tags));
    }

    @Override
    public int hashCode() {
        // use this method for custom fields hashing instead of implementing your own
        //return Objects.hash(persons, tags);
        return Objects.hash(persons, favouritePersons, tags);
    }
}

```
###### \src\main\java\seedu\address\model\Model.java
``` java
    /** Deletes the given person from Favourite List. */
    void removeFavouritePerson(ReadOnlyPerson target) throws PersonNotFoundException;
```
###### \src\main\java\seedu\address\model\Model.java
``` java

    /** Adds the given person */
    void addPerson(ReadOnlyPerson person) throws DuplicatePersonException;

```
###### \src\main\java\seedu\address\model\Model.java
``` java
    /** Adds the given person into Favourite List */
    void addFavouritePerson(ReadOnlyPerson person) throws DuplicatePersonException;
```
###### \src\main\java\seedu\address\model\Model.java
``` java

    /**
     * Replaces the given person {@code target} with {@code editedPerson}.
     *
     * @throws DuplicatePersonException if updating the person's details causes the person to be equivalent to
     *      another existing person in the list.
     * @throws PersonNotFoundException if {@code target} could not be found in the list.
     */
    void updatePerson(ReadOnlyPerson target, ReadOnlyPerson editedPerson)
            throws DuplicatePersonException, PersonNotFoundException;

```
###### \src\main\java\seedu\address\model\Model.java
``` java
    String getCurrentList();

    void setCurrentList(String currentList);
```
###### \src\main\java\seedu\address\model\Model.java
``` java

    /** Returns an unmodifiable view of the filtered person list */
    ObservableList<ReadOnlyPerson> getFilteredPersonList();

```
###### \src\main\java\seedu\address\model\Model.java
``` java
    /** Returns an unmodifiable view of the filtered favourite person list */
    ObservableList<ReadOnlyPerson> getFilteredFavouritePersonList();

    /** Sorts the list in alphabhetical order of names */
    void sortFilteredPersonListName();

    /** Sorts the list in ascending order of birthdays : Jan to Dec */
    void sortFilteredPersonListBirthday();
```
###### \src\main\java\seedu\address\model\Model.java
``` java

    /**
     * Updates the filter of the filtered person list to filter by the given {@code predicate}.
     * @throws NullPointerException if {@code predicate} is null.
     */
    void updateFilteredPersonList(Predicate<ReadOnlyPerson> predicate);

```
###### \src\main\java\seedu\address\model\Model.java
``` java
    void updateFilteredFavouritePersonList(Predicate<ReadOnlyPerson> predicate);

    void changeListTo(String listName);
```
###### \src\main\java\seedu\address\model\Model.java
``` java
}
```
###### \src\main\java\seedu\address\model\ModelManager.java
``` java
    private final FilteredList<ReadOnlyPerson> filteredFavouritePersons;

    private String currentList;
```
###### \src\main\java\seedu\address\model\ModelManager.java
``` java

    /**
     * Initializes a ModelManager with the given addressBook and userPrefs.
     */
    public ModelManager(ReadOnlyAddressBook addressBook, UserPrefs userPrefs) {
        super();
        requireAllNonNull(addressBook, userPrefs);

        logger.fine("Initializing with address book: " + addressBook + " and user prefs " + userPrefs);

        this.addressBook = new AddressBook(addressBook);
        filteredPersons = new FilteredList<>(this.addressBook.getPersonList());
```
###### \src\main\java\seedu\address\model\ModelManager.java
``` java
        filteredFavouritePersons = new FilteredList<>(this.addressBook.getFavouritePersonList());
```
###### \src\main\java\seedu\address\model\ModelManager.java
``` java
        this.currentList = "list";
    }

    public ModelManager() {
        this(new AddressBook(), new UserPrefs());
    }

    @Override
    public void resetData(ReadOnlyAddressBook newData) {
        addressBook.resetData(newData);
        indicateAddressBookChanged();
    }

    @Override
    public ReadOnlyAddressBook getAddressBook() {
        return addressBook;
    }

    /** Raises an event to indicate the model has changed */
    private void indicateAddressBookChanged() {
        raise(new AddressBookChangedEvent(addressBook));
    }

    @Override
    public synchronized void deletePerson(ReadOnlyPerson target) throws PersonNotFoundException {
        addressBook.removePerson(target);
        indicateAddressBookChanged();
    }

```
###### \src\main\java\seedu\address\model\ModelManager.java
``` java
    @Override
    public synchronized void removeFavouritePerson(ReadOnlyPerson person) throws PersonNotFoundException {
        addressBook.removeFavouritePerson(person);
        updateFilteredPersonList(PREDICATE_SHOW_ALL_PERSONS);
        indicateAddressBookChanged();
    }
```
###### \src\main\java\seedu\address\model\ModelManager.java
``` java

    @Override
    public synchronized void addPerson(ReadOnlyPerson person) throws DuplicatePersonException {
        addressBook.addPerson(person);
        updateFilteredPersonList(PREDICATE_SHOW_ALL_PERSONS);
        indicateAddressBookChanged();
    }

```
###### \src\main\java\seedu\address\model\ModelManager.java
``` java
    @Override
    public synchronized void addFavouritePerson(ReadOnlyPerson person) throws DuplicatePersonException {
        addressBook.addFavouritePerson(person);
        updateFilteredPersonList(PREDICATE_SHOW_ALL_PERSONS);
        indicateAddressBookChanged();
    }
```
###### \src\main\java\seedu\address\model\ModelManager.java
``` java

    @Override
    public void updatePerson(ReadOnlyPerson target, ReadOnlyPerson editedPerson)
            throws DuplicatePersonException, PersonNotFoundException {
        requireAllNonNull(target, editedPerson);

        addressBook.updatePerson(target, editedPerson);
        indicateAddressBookChanged();
    }

```
###### \src\main\java\seedu\address\model\ModelManager.java
``` java
    @Override
    public void changeListTo(String listName) {
        raise(new ChangeInternalListEvent(listName));
    }

    @Override
    public String getCurrentList() {
        return currentList;
    }

    @Override
    public void setCurrentList(String currentList) {
        this.currentList =  currentList;
    }
```
###### \src\main\java\seedu\address\model\ModelManager.java
``` java

    //=========== Filtered Person List Accessors =============================================================

    /**
     * Returns an unmodifiable view of the list of {@code ReadOnlyPerson} backed by the internal list of
     * {@code addressBook}
     */
    @Override
    public ObservableList<ReadOnlyPerson> getFilteredPersonList() {
        setCurrentList("list");
        return FXCollections.unmodifiableObservableList(filteredPersons);
    }

```
###### \src\main\java\seedu\address\model\ModelManager.java
``` java
    @Override
    public ObservableList<ReadOnlyPerson> getFilteredFavouritePersonList() {
        setCurrentList("favlist");
        return FXCollections.unmodifiableObservableList(filteredFavouritePersons);
    }
```
###### \src\main\java\seedu\address\model\ModelManager.java
``` java

    @Override
    public void updateFilteredPersonList(Predicate<ReadOnlyPerson> predicate) {
        requireNonNull(predicate);
        filteredPersons.setPredicate(predicate);
    }

```
###### \src\main\java\seedu\address\model\ModelManager.java
``` java
    @Override
    public void updateFilteredFavouritePersonList(Predicate<ReadOnlyPerson> predicate) {
        requireNonNull(predicate);
        filteredFavouritePersons.setPredicate(predicate);
    }

    @Override
    public void sortFilteredPersonListName() {
        addressBook.sortPersonsByName();
        indicateAddressBookChanged();
    }

    @Override
    public void sortFilteredPersonListBirthday() {
        addressBook.sortPersonsByBirthday();
        indicateAddressBookChanged();
    }
```
###### \src\main\java\seedu\address\model\ModelManager.java
``` java

    @Override
    public boolean equals(Object obj) {
        // short circuit if same object
        if (obj == this) {
            return true;
        }

        // instanceof handles nulls
        if (!(obj instanceof ModelManager)) {
            return false;
        }

        // state check
        ModelManager other = (ModelManager) obj;
        return addressBook.equals(other.addressBook)
                && filteredPersons.equals(other.filteredPersons);
    }

}
```
###### \src\main\java\seedu\address\model\person\Birthday.java
``` java
package seedu.address.model.person;

import static java.util.Objects.requireNonNull;

import seedu.address.commons.exceptions.IllegalValueException;

/**
 * Represents a Person's birthday in the address book.
 * Guarantees: immutable; is valid as declared in {@link #isValidBirthday(String)}
 */
public class Birthday {

    public static final String MESSAGE_BIRTHDAY_CONSTRAINTS =
            "Day, Month and Year should be in DD/MM/YYYY format. Must be a valid date.";

    public static final String BIRTHDAY_VALIDATION_REGEX = "^(?:(?:31(\\/|-|\\.)(?:0?[13578]|1[02]))\\1|(?:(?:29|30)"
            + "(\\/|-|\\.)(?:0?[1,3-9]|1[0-2])\\2))(?:(?:1[6-9]|[2-9]\\d)?\\d{2})$|^(?:29(\\/|-|\\.)0?2"
            + "\\3(?:(?:(?:1[6-9]|[2-9]\\d)?(?:0[48]|[2468][048]|[13579][26])|(?:(?:16|[2468][048]|[3579]"
            + "[26])00))))$|^(?:0?[1-9]|1\\d|2[0-8])(\\/|-|\\.)(?:(?:0?[1-9])|(?:1[0-2]))\\4(?:(?:1[6-9]|"
            + "[2-9]\\d)?\\d{2})$";

    public final String value;

    /**
     * Validates given date.
     *
     * @throws IllegalValueException if given birthday string is invalid.
     */
    public Birthday(String birthday) throws IllegalValueException {
        requireNonNull(birthday);
        String trimmedBirthday = birthday.trim();
        if (trimmedBirthday.equals("valueNotFound")) {
            this.value = "No Birthday Listed";
        } else {
            if (!isValidBirthday(trimmedBirthday)) {
                throw new IllegalValueException(MESSAGE_BIRTHDAY_CONSTRAINTS);
            }
            this.value = trimmedBirthday;
        }
    }

    /**
     * Returns true if a given string is a valid person birthday.
     */
    public static boolean isValidBirthday(String test) {
        return test.matches(BIRTHDAY_VALIDATION_REGEX);
    }

    @Override
    public String toString() {
        return value;
    }

    @Override
    public boolean equals(Object other) {
        return other == this // short circuit if same object
                || (other instanceof Birthday // instanceof handles nulls
                && this.value.equals(((Birthday) other).value)); // state check
    }

    @Override
    public int hashCode() {
        return value.hashCode();
    }
}
```
###### \src\main\java\seedu\address\model\person\Birthday.java
``` java

```
###### \src\main\java\seedu\address\model\person\NameContainsKeywordsPredicate.java
``` java
        Set<String> s1 = new HashSet<String>(keywords);
        String[] tagList = person.getOnlyTags().split(" ");
        Set<String> s2 = new HashSet<String>(Arrays.asList(tagList));

        return ((keywords.stream()
                .anyMatch(keyword -> StringUtil.containsWordIgnoreCase(person.getName().fullName, keyword)))
                || (!Collections.disjoint(s2, s1))) || (keywords.stream().anyMatch(keyword ->
                StringUtil.containsSubstringOfWord(person.getName().fullName, keyword)));
```
###### \src\main\java\seedu\address\model\person\NameContainsKeywordsPredicate.java
``` java
    }

    @Override
    public boolean equals(Object other) {
        return other == this // short circuit if same object
                || (other instanceof NameContainsKeywordsPredicate // instanceof handles nulls
                && this.keywords.equals(((NameContainsKeywordsPredicate) other).keywords)); // state check
    }

}
```
###### \src\main\java\seedu\address\model\person\Person.java
``` java
        this.birthday = new SimpleObjectProperty<>(birthday);
```
###### \src\main\java\seedu\address\model\person\Person.java
``` java
        this.email = new SimpleObjectProperty<>(email);
        this.address = new SimpleObjectProperty<>(address);
        this.score = new SimpleObjectProperty<>(score);
        // protect internal tags from changes in the arg list
        this.tags = new SimpleObjectProperty<>(new UniqueTagList(tags));
    }

    /**
     * Creates a copy of the given ReadOnlyPerson, which is nice.
     */
    public Person(ReadOnlyPerson source) {
        this(source.getName(), source.getPhone(), source.getBirthday(), source.getEmail(),
                source.getAddress(), source.getScore(), source.getTags());
    }

    public void setName(Name name) {
        this.name.set(requireNonNull(name));
    }

    @Override
    public ObjectProperty<Name> nameProperty() {
        return name;
    }

    @Override
    public Name getName() {
        return name.get();
    }

    public void setPhone(Phone phone) {
        this.phone.set(requireNonNull(phone));
    }

    @Override
    public ObjectProperty<Phone> phoneProperty() {
        return phone;
    }

    @Override
    public Phone getPhone() {
        return phone.get();
    }

```
###### \src\main\java\seedu\address\model\person\Person.java
``` java
    public void setBirthday(Birthday birthday)  {
        this.birthday.set(requireNonNull(birthday));
    }

    @Override
    public ObjectProperty<Birthday> birthdayProperty()  {
        return birthday;
    }

    @Override
    public Birthday getBirthday() {
        return birthday.get();
    }
```
###### \src\main\java\seedu\address\model\person\Person.java
``` java

    public void setEmail(Email email) {
        this.email.set(requireNonNull(email));
    }

    @Override
    public ObjectProperty<Email> emailProperty() {
        return email;
    }

    @Override
    public Email getEmail() {
        return email.get();
    }

    public void setAddress(Address address) {
        this.address.set(requireNonNull(address));
    }

    @Override
    public ObjectProperty<Address> addressProperty() {
        return address;
    }

    @Override
    public Address getAddress() {
        return address.get();
    }
```
###### \src\main\java\seedu\address\model\person\ReadOnlyPerson.java
``` java
    ObjectProperty<Birthday> birthdayProperty();
    Birthday getBirthday();
```
###### \src\main\java\seedu\address\model\person\ReadOnlyPerson.java
``` java
    ObjectProperty<Email> emailProperty();
    Email getEmail();
    ObjectProperty<Address> addressProperty();
    Address getAddress();
    ObjectProperty<Score> scoreProperty();
    Score getScore();
    ObjectProperty<UniqueTagList> tagProperty();
    Set<Tag> getTags();

    /**
     * Returns true if both have the same state. (interfaces cannot override .equals)
     */
    default boolean isSameStateAs(ReadOnlyPerson other) {
        return other == this // short circuit if same object
                || (other != null // this is first to avoid NPE below
                && other.getName().equals(this.getName()) // state checks here onwards
                && other.getPhone().equals(this.getPhone())
                && other.getBirthday().equals(this.getBirthday())
                && other.getEmail().equals(this.getEmail())
                && other.getAddress().equals(this.getAddress()));
    }

    /**
     * Formats the person as text, showing all contact details.
     */
    default String getAsText() {
        final StringBuilder builder = new StringBuilder();
        builder.append(getName())
                .append(" Phone: ")
                .append(getPhone())
```
###### \src\main\java\seedu\address\model\person\ReadOnlyPerson.java
``` java
                .append(" Birthday: ")
                .append(getBirthday())
```
###### \src\main\java\seedu\address\model\person\ReadOnlyPerson.java
``` java
                .append(" Email: ")
                .append(getEmail())
                .append(" Address: ")
                .append(getAddress())
```
###### \src\main\java\seedu\address\model\person\UniquePersonList.java
``` java
    /**
     * Sorts the list of people in alphabhetical order of names.
     */
    public void sortPersonsByName() {

        Comparator<ReadOnlyPerson> personComparator = new Comparator<ReadOnlyPerson>() {

            public int compare(ReadOnlyPerson person1, ReadOnlyPerson person2) {

                String personName1 = person1.getScore().toString();
                String personName2 = person2.getScore().toString();

                return personName2.compareTo(personName1);
            }

        };

        FXCollections.sort(internalList, personComparator);
    }
```
###### \src\main\java\seedu\address\model\person\UniquePersonList.java
``` java

    /**
     * Sorts the list of people in order of birthdays: Jan to Dec.
     */
    public void sortPersonsByBirthday() {

        Comparator<ReadOnlyPerson> personComparator = new Comparator<ReadOnlyPerson>() {

            public int compare(ReadOnlyPerson person1, ReadOnlyPerson person2) {


                SimpleDateFormat sdf = new SimpleDateFormat("MM/dd");

                String[] day1 = person1.getBirthday().toString().split("/");
                String[] day2 = person2.getBirthday().toString().split("/");

                String date1 = day1[1] + "/" + day1[0];
                String date2 = day2[1] + "/" + day2[0];

                Date birthday1 = null;
                Date birthday2 = null;
                sdf.setLenient(false);
                try {
                    birthday1 = sdf.parse(date1);
                    birthday2 = sdf.parse(date2);
                } catch (ParseException e) {
                    e.printStackTrace();
                }
                return birthday1.compareTo(birthday2);
            }

        };

        FXCollections.sort(internalList, personComparator);
    }

    public void setPersons(UniquePersonList replacement) {
        this.internalList.setAll(replacement.internalList);
    }

    public void setPersons(List<? extends ReadOnlyPerson> persons) throws DuplicatePersonException {
        final UniquePersonList replacement = new UniquePersonList();
        for (final ReadOnlyPerson person : persons) {
            replacement.add(new Person(person));
        }
        setPersons(replacement);
    }

    /**
     * Returns the backing list as an unmodifiable {@code ObservableList}.
     */
    public ObservableList<ReadOnlyPerson> asObservableList() {
        return FXCollections.unmodifiableObservableList(mappedList);
    }

    @Override
    public Iterator<Person> iterator() {
        return internalList.iterator();
    }

    @Override
    public boolean equals(Object other) {
        return other == this // short circuit if same object
                || (other instanceof UniquePersonList // instanceof handles nulls
                        && this.internalList.equals(((UniquePersonList) other).internalList));
    }

    @Override
    public int hashCode() {
        return internalList.hashCode();
    }
}
```
###### \src\main\java\seedu\address\model\util\SampleDataUtil.java
``` java
                new Person(new Name("Alex Yeoh"), new Phone("87438807"), new Birthday("16/08/1968"),
                new Email("alexyeoh@example.com"), new Address("Blk 30 Geylang Street 29, #06-40"),
                new Score("8"),
                    getTagSet("friends")),
                new Person(new Name("Bernice Yu"), new Phone("99272758"),  new Birthday("21/04/1973"),
                        new Email("berniceyu@example.com"),
                    new Address("Blk 30 Lorong 3 Serangoon Gardens, #07-18"), new Score("5"),
                    getTagSet("colleagues", "friends")),
                new Person(new Name("Charlotte Oliveiro"), new Phone("93210283"),  new Birthday("11/01/1999"),
                        new Email("charlotte@example.com"),
                    new Address("Blk 11 Ang Mo Kio Street 74, #11-04"), new Score("9"),
                    getTagSet("neighbours")),
                new Person(new Name("David Li"), new Phone("91031282"),  new Birthday("17/07/2006"),
                        new Email("lidavid@example.com"),
                    new Address("Blk 436 Serangoon Gardens Street 26, #16-43"), new Score("2"),
                    getTagSet("family")),
                new Person(new Name("Irfan Ibrahim"), new Phone("92492021"),  new Birthday("31/05/1936"),
                        new Email("irfan@example.com"),
                    new Address("Blk 47 Tampines Street 20, #17-35"), new Score("1"),
                    getTagSet("classmates")),
                new Person(new Name("Roy Balakrishnan"), new Phone("92624417"),  new Birthday("7/09/1995"),
                        new Email("royb@example.com"),
                    new Address("Blk 45 Aljunied Street 85, #11-31"), new Score("3"),
                    getTagSet("colleagues"))
```
###### \src\main\java\seedu\address\model\util\SampleDataUtil.java
``` java
            };
        } catch (IllegalValueException e) {
            throw new AssertionError("sample data cannot be invalid", e);
        }
    }

    public static ReadOnlyAddressBook getSampleAddressBook() {
        try {
            AddressBook sampleAb = new AddressBook();
            for (Person samplePerson : getSamplePersons()) {
                sampleAb.addPerson(samplePerson);
            }
            return sampleAb;
        } catch (DuplicatePersonException e) {
            throw new AssertionError("sample data cannot contain duplicate persons", e);
        }
    }

    /**
     * Returns a tag set containing the list of strings given.
     */
    public static Set<Tag> getTagSet(String... strings) throws IllegalValueException {
        HashSet<Tag> tags = new HashSet<>();
        for (String s : strings) {
            tags.add(new Tag(s));
        }

        return tags;
    }

}
```
###### \src\main\java\seedu\address\storage\XmlAdaptedPerson.java
``` java
    private String birthday;
    @XmlElement(required = true)
```
###### \src\main\java\seedu\address\storage\XmlAdaptedPerson.java
``` java
    private String email;
    @XmlElement(required = true)
    private String address;

    @XmlElement
    private String score;

    @XmlElement
    private List<XmlAdaptedTag> tagged = new ArrayList<>();

    /**
     * Constructs an XmlAdaptedPerson.
     * This is the no-arg constructor that is required by JAXB.
     */
    public XmlAdaptedPerson() {}


    /**
     * Converts a given Person into this class for JAXB use.
     *
     * @param source future changes to this will not affect the created XmlAdaptedPerson
     */
    public XmlAdaptedPerson(ReadOnlyPerson source) {
        name = source.getName().fullName;
        phone = source.getPhone().value;
```
###### \src\main\java\seedu\address\storage\XmlAdaptedPerson.java
``` java
        birthday = source.getBirthday().value;
```
###### \src\main\java\seedu\address\storage\XmlAdaptedPerson.java
``` java
        email = source.getEmail().value;
        address = source.getAddress().value;
        score = source.getScore().value;
        tagged = new ArrayList<>();
        for (Tag tag : source.getTags()) {
            tagged.add(new XmlAdaptedTag(tag));
        }
    }

    /**
     * Converts this jaxb-friendly adapted person object into the model's Person object.
     *
     * @throws IllegalValueException if there were any data constraints violated in the adapted person
     */
    public Person toModelType() throws IllegalValueException {
        final List<Tag> personTags = new ArrayList<>();
        for (XmlAdaptedTag tag : tagged) {
            personTags.add(tag.toModelType());
        }
        final Name name = new Name(this.name);
        final Phone phone = new Phone(this.phone);
        final Birthday birthday = new Birthday(this.birthday);
        final Email email = new Email(this.email);
        final Address address = new Address(this.address);
        final Score score = new Score(this.score);
        final Set<Tag> tags = new HashSet<>(personTags);
        return new Person(name, phone, birthday, email, address, score, tags);
    }
}
```
###### \src\main\java\seedu\address\storage\XmlSerializableAddressBook.java
``` java
        favouritePersons.addAll(src.getFavouritePersonList().stream().map(XmlAdaptedPerson::new)
                .collect(Collectors.toList()));
```
###### \src\main\java\seedu\address\storage\XmlSerializableAddressBook.java
``` java
        tags.addAll(src.getTagList().stream().map(XmlAdaptedTag::new).collect(Collectors.toList()));
    }

    @Override
    public ObservableList<ReadOnlyPerson> getPersonList() {
        final ObservableList<ReadOnlyPerson> persons = this.persons.stream().map(p -> {
            try {
                return p.toModelType();
            } catch (IllegalValueException e) {
                e.printStackTrace();
                //TODO: better error handling
                return null;
            }
        }).collect(Collectors.toCollection(FXCollections::observableArrayList));
        return FXCollections.unmodifiableObservableList(persons);
    }

```
###### \src\main\java\seedu\address\storage\XmlSerializableAddressBook.java
``` java
    @Override
    public ObservableList<ReadOnlyPerson> getFavouritePersonList() {
        final ObservableList<ReadOnlyPerson> favouritePersons = this.favouritePersons.stream().map(p -> {
            try {
                return p.toModelType();
            } catch (IllegalValueException e) {
                e.printStackTrace();
                //TODO: better error handling
                return null;
            }
        }).collect(Collectors.toCollection(FXCollections::observableArrayList));
        return FXCollections.unmodifiableObservableList(favouritePersons);
    }
```
###### \src\main\java\seedu\address\storage\XmlSerializableAddressBook.java
``` java

    @Override
    public ObservableList<Tag> getTagList() {
        final ObservableList<Tag> tags = this.tags.stream().map(t -> {
            try {
                return t.toModelType();
            } catch (IllegalValueException e) {
                e.printStackTrace();
                //TODO: better error handling
                return null;
            }
        }).collect(Collectors.toCollection(FXCollections::observableArrayList));
        return FXCollections.unmodifiableObservableList(tags);
    }

}
```
###### \src\main\java\seedu\address\ui\ChangeInternalListEvent.java
``` java
package seedu.address.ui;

import seedu.address.commons.events.BaseEvent;

/**
 * Creates an event to change the Internal List
 */
public class ChangeInternalListEvent extends BaseEvent {

    //private String listName;
    private final String listName;

    public ChangeInternalListEvent(String listName) {
        this.listName = listName;
    }

    public String getListName() {
        return listName;
    }

    @Override
    public String toString() {
        return this.getClass().getSimpleName();
    }
}
```
###### \src\main\java\seedu\address\ui\ChangeInternalListEvent.java
``` java

```
###### \src\main\java\seedu\address\ui\CommandBox.java
``` java
    /**
     * handles button events given to it by the fxml document for which it is set as controller by
     * a constructor in UiPart. handleFavListButton event handles the event when the Favlist button
     * containing a 'star' icon to represent a fav list is clicked.
     * @param buttonEvent
     */
    @FXML
    private void handleFavlistButtonAction(ActionEvent buttonEvent) {
        try {
            CommandResult commandResult = logic.execute("favlist");
            logger.info("Result: " + commandResult.feedbackToUser);
            raise(new NewResultAvailableEvent(commandResult.feedbackToUser));
        } catch (CommandException | ParseException e) {
            // handling command failure
            logger.info("Delete call failed on index favlist");
            raise(new NewResultAvailableEvent(e.getMessage()));
        }
    }
```
###### \src\main\java\seedu\address\ui\CommandBox.java
``` java
}
```
###### \src\main\java\seedu\address\ui\MainWindow.java
``` java
    /**
     * Changes displayed list accordingly
     */
    void fillInnerPartsWithIndicatedList(String listname) {
        switch(listname) {
        case "fl":
        case "favlist":
            personListPanel = new PersonListPanel(logic.getFilteredFavoritePersonList(), logic);
            break;

        default:
            personListPanel = new PersonListPanel(logic.getFilteredPersonList(), logic);
        }
        personListPanelPlaceholder.getChildren().add(personListPanel.getRoot());
    }
```
###### \src\main\java\seedu\address\ui\MainWindow.java
``` java

    void hide() {
        primaryStage.hide();
    }

    private void setTitle(String appTitle) {
        primaryStage.setTitle(appTitle);
    }

    /**
     * Sets the given image as the icon of the main window.
     * @param iconSource e.g. {@code "/images/help_icon.png"}
     */
    private void setIcon(String iconSource) {
        FxViewUtil.setStageIcon(primaryStage, iconSource);
    }

    /**
     * Sets the default size based on user preferences.
     */
    private void setWindowDefaultSize(UserPrefs prefs) {
        primaryStage.setHeight(prefs.getGuiSettings().getWindowHeight());
        primaryStage.setWidth(prefs.getGuiSettings().getWindowWidth());
        if (prefs.getGuiSettings().getWindowCoordinates() != null) {
            primaryStage.setX(prefs.getGuiSettings().getWindowCoordinates().getX());
            primaryStage.setY(prefs.getGuiSettings().getWindowCoordinates().getY());
        }
    }

    private void setWindowMinSize() {
        primaryStage.setMinHeight(MIN_HEIGHT);
        primaryStage.setMinWidth(MIN_WIDTH);
    }

    /**
     * Returns the current size and the position of the main Window.
     */
    GuiSettings getCurrentGuiSetting() {
        return new GuiSettings(primaryStage.getWidth(), primaryStage.getHeight(),
                (int) primaryStage.getX(), (int) primaryStage.getY());
    }

    /**
     * Opens the help window.
     */
    @FXML
    public void handleHelp() {
        HelpWindow helpWindow = new HelpWindow();
        helpWindow.show();
    }

    void show() {
        primaryStage.show();
    }

    /**
     * Closes the application.
     */
    @FXML
    private void handleExit() {
        raise(new ExitAppRequestEvent());
    }

```
###### \src\main\java\seedu\address\ui\PersonCard.java
``` java
    @FXML
    private Label birthday;
```
###### \src\main\java\seedu\address\ui\PersonCard.java
``` java
    @FXML
    private Label address;
    @FXML
    private Label email;
    @FXML
    private Label score;
    @FXML
    private FlowPane tags;

```
###### \src\main\java\seedu\address\ui\PersonCard.java
``` java
        birthday.textProperty().bind(Bindings.convert(person.birthdayProperty()));
```
###### \src\main\java\seedu\address\ui\PersonCard.java
``` java
        address.textProperty().bind(Bindings.convert(person.addressProperty()));
        email.textProperty().bind(Bindings.convert(person.emailProperty()));
        score.textProperty().bind(Bindings.convert(person.scoreProperty()));
        person.tagProperty().addListener((observable, oldValue, newValue) -> {
            tags.getChildren().clear();
            initTags(person);
        });
    }

    /**
     * Initializes color tags
     * initializes tags for the person
     * @param person
     */
    private void initTags(ReadOnlyPerson person) {
        person.getTags().forEach(tag -> {
            Label tagLabel = new Label(tag.tagName);
            tagLabel.setStyle("-fx-background-color: " + mapTagToColor(tag.tagName));
            tags.getChildren().add(tagLabel);
        });
        //person.getTags().forEach(tag -> tags.getChildren().add(new Label(tag.tagName)));
    }

    /**
     * checks equality to the person
     * @param other
     * @return if the person equals the param
     */
    @Override
    public boolean equals(Object other) {
        // short circuit if same object
        if (other == this) {
            return true;
        }
        // instanceof handles nulls
        if (!(other instanceof PersonCard)) {
            return false;
        }

        // state check
        PersonCard card = (PersonCard) other;
        return id.getText().equals(card.id.getText())
                && person.equals(card.person);
    }
```
###### \src\main\java\seedu\address\ui\PersonCard.java
``` java
            if (logic.getCurrentList().contains("favlist")) {
                commandResult = new CommandResult("Delete command does not work in favourite list");;
            } else {
                commandResult = logic.execute(delCommand);
            }
```
###### \src\main\java\seedu\address\ui\PersonCard.java
``` java

```
###### \src\main\java\seedu\address\ui\PersonCard.java
``` java
        CommandResult commandResult = new CommandResult("");
        if (logic.getCurrentList().contains("favlist")) {
            commandResult = new CommandResult("Edit command does not work in favourite list");;
```
###### \src\main\java\seedu\address\ui\PersonCard.java
``` java

```
###### \src\main\java\seedu\address\ui\UiManager.java
``` java
    @Subscribe
    private void handleChangeInternalListEvent(ChangeInternalListEvent event) {
        logger.info(LogsCenter.getEventHandlingLogMessage(event));
        mainWindow.fillInnerPartsWithIndicatedList(event.getListName());
    }
```
###### \src\main\java\seedu\address\ui\UiManager.java
``` java
}

```
###### \src\test\java\guitests\guihandles\PersonCardHandle.java
``` java
    private static final String BIRTHDAY_FIELD_ID = "#birthday";
```
###### \src\test\java\guitests\guihandles\PersonCardHandle.java
``` java
    private static final String EMAIL_FIELD_ID = "#email";
    private static final String TAGS_FIELD_ID = "#tags";

    private final Label idLabel;
    private final Label nameLabel;
    private final Label addressLabel;
    private final Label phoneLabel;
    private final Label birthdayLabel;
    private final Label emailLabel;
    private final List<Label> tagLabels;

    public PersonCardHandle(Node cardNode) {
        super(cardNode);

        this.idLabel = getChildNode(ID_FIELD_ID);
        this.nameLabel = getChildNode(NAME_FIELD_ID);
        this.addressLabel = getChildNode(ADDRESS_FIELD_ID);
        this.phoneLabel = getChildNode(PHONE_FIELD_ID);
```
###### \src\test\java\guitests\guihandles\PersonCardHandle.java
``` java
        this.birthdayLabel = getChildNode(BIRTHDAY_FIELD_ID);
```
###### \src\test\java\guitests\guihandles\PersonCardHandle.java
``` java
        this.emailLabel = getChildNode(EMAIL_FIELD_ID);

        Region tagsContainer = getChildNode(TAGS_FIELD_ID);
        this.tagLabels = tagsContainer
                .getChildrenUnmodifiable()
                .stream()
                .map(Label.class::cast)
                .collect(Collectors.toList());
    }

    public String getId() {
        return idLabel.getText();
    }

    public String getName() {
        return nameLabel.getText();
    }

    public String getAddress() {
        return addressLabel.getText();
    }

    public String getPhone() {
        return phoneLabel.getText();
    }

```
###### \src\test\java\guitests\guihandles\PersonCardHandle.java
``` java
    public String getBirthday()  {
        return birthdayLabel.getText();
    }
```
###### \src\test\java\guitests\guihandles\PersonCardHandle.java
``` java

    public String getEmail() {
        return emailLabel.getText();
    }

    public List<String> getTags() {
        return tagLabels
                .stream()
                .map(Label::getText)
                .collect(Collectors.toList());
    }
}
```
###### \src\test\java\seedu\address\commons\util\StringUtilTest.java
``` java
    @Test
    public void containsSubstringOfWord_emptyWord_throwsIllegalArgumentException() {
        assertExceptionThrown(IllegalArgumentException.class, "Normal sentence", "  ",
                Optional.of("Word parameter cannot be empty"));
    }

    @Test
    public void containsSubstringOfWord_noSentence_throwsNullPointerException() {
        assertExceptionThrown(NullPointerException.class, null, "Alice", Optional.empty());
    }

    @Test
    public void containsSubstringOfWord_multipleWords_throwsIllegalArgumentException() {
        assertExceptionThrown(IllegalArgumentException.class, "Normal sentence", "Alice John",
                Optional.of("Word parameter should be a single word"));
    }

    @Test
    public void containsSubstringOfWord_validInputs_correctResult() {

        // Empty sentences
        assertFalse(StringUtil.containsSubstringOfWord("", "Alice"));
        assertFalse(StringUtil.containsSubstringOfWord("    ", "987"));

        // Matches multiple words
        assertTrue(StringUtil.containsWordIgnoreCase("Alice John Johnny", "john"));

        // Matches partial words and complete words (finding by substring is also case-insensitive)
        assertTrue(StringUtil.containsSubstringOfWord("Alice John agatha", "ag"));
        assertTrue(StringUtil.containsSubstringOfWord("Alice John agatha", "Al")); // First word in sentence
        assertTrue(StringUtil.containsSubstringOfWord("Alice John agatha", "  agatha ")); // trailing spaces
        assertTrue(StringUtil.containsSubstringOfWord("Alice John agatha", "agatha")); // Last word
        assertTrue(StringUtil.containsSubstringOfWord("Alice", "alice")); // one word
        assertFalse(StringUtil.containsSubstringOfWord("Alicia John carLo", "Johnny"));

    }
```
###### \src\test\java\seedu\address\commons\util\StringUtilTest.java
``` java

    //---------------- Tests for getDetails --------------------------------------

    /*
     * Equivalence Partitions: null, valid throwable object
     */

    @Test
    public void getDetails_exceptionGiven() {
        assertThat(StringUtil.getDetails(new FileNotFoundException("file not found")),
                   containsString("java.io.FileNotFoundException: file not found"));
    }

    @Test
    public void getDetails_nullGiven_throwsNullPointerException() {
        thrown.expect(NullPointerException.class);
        StringUtil.getDetails(null);
    }


}
```
###### \src\test\java\seedu\address\logic\commands\AddCommandTest.java
``` java
        @Override
        public void sortFilteredPersonListName() {
            fail("This method should not be called.");
        }

        @Override
        public void sortFilteredPersonListBirthday() {
            fail("This method should not be called.");
        }

        @Override
        public void addFavouritePerson(ReadOnlyPerson target) {
            fail("This method should not be called.");
        }

        @Override
        public void removeFavouritePerson(ReadOnlyPerson target) {
            fail("This method should not be called.");
        }

        @Override
        public void changeListTo(String listName) {
            fail("This method should not be called.");
        }

        @Override
        public void setCurrentList(String currentList)  {
            fail("This method should not be called.");
        }

        @Override
        public String getCurrentList() {
            fail("This method should not be called.");
            return null;
        }

        @Override
        public void updateFilteredFavouritePersonList(Predicate<ReadOnlyPerson> predicate) {
            fail("This method should not be called.");
        }

        @Override
        public ObservableList<ReadOnlyPerson> getFilteredFavouritePersonList() {
            fail("This method should not be called.");
            return null;
        }
```
###### \src\test\java\seedu\address\logic\commands\AddCommandTest.java
``` java

        @Override
        public void deletePerson(ReadOnlyPerson target) throws PersonNotFoundException {
            fail("This method should not be called.");
        }

        @Override
        public void updatePerson(ReadOnlyPerson target, ReadOnlyPerson editedPerson)
                throws DuplicatePersonException {
            fail("This method should not be called.");
        }

        @Override
        public ObservableList<ReadOnlyPerson> getFilteredPersonList() {
            fail("This method should not be called.");
            return null;
        }

        @Override
        public void updateFilteredPersonList(Predicate<ReadOnlyPerson> predicate) {
            fail("This method should not be called.");
        }
    }

    /**
     * A Model stub that always throw a DuplicatePersonException when trying to add a person.
     */
    private class ModelStubThrowingDuplicatePersonException extends ModelStub {
        @Override
        public void addPerson(ReadOnlyPerson person) throws DuplicatePersonException {
            throw new DuplicatePersonException();
        }

        @Override
        public ReadOnlyAddressBook getAddressBook() {
            return new AddressBook();
        }
    }

    /**
     * A Model stub that always accept the person being added.
     */
    private class ModelStubAcceptingPersonAdded extends ModelStub {
        final ArrayList<Person> personsAdded = new ArrayList<>();

        @Override
        public void addPerson(ReadOnlyPerson person) throws DuplicatePersonException {
            personsAdded.add(new Person(person));
        }

        @Override
        public ReadOnlyAddressBook getAddressBook() {
            return new AddressBook();
        }
    }

}
```
###### \src\test\java\seedu\address\logic\commands\CommandTestUtil.java
``` java
    public static final String VALID_BIRTHDAY_AMY = "21/04/1973";
    public static final String VALID_BIRTHDAY_BOB = "16/08/1968";
```
###### \src\test\java\seedu\address\logic\commands\CommandTestUtil.java
``` java
    public static final String VALID_EMAIL_AMY = "amy@example.com";
    public static final String VALID_EMAIL_BOB = "bob@example.com";
    public static final String VALID_ADDRESS_AMY = "Block 312, Amy Street 1";
    public static final String VALID_ADDRESS_BOB = "Block 123, Bobby Street 3";
    public static final String VALID_SCORE_AMY = "8";
    public static final String VALID_SCORE_BOB = "2";
    public static final String VALID_TAG_HUSBAND = "husband";
    public static final String VALID_TAG_FRIEND = "friend";

    public static final String NAME_DESC_AMY = " " + PREFIX_NAME + VALID_NAME_AMY;
    public static final String NAME_DESC_BOB = " " + PREFIX_NAME + VALID_NAME_BOB;
    public static final String PHONE_DESC_AMY = " " + PREFIX_PHONE + VALID_PHONE_AMY;
    public static final String PHONE_DESC_BOB = " " + PREFIX_PHONE + VALID_PHONE_BOB;
```
###### \src\test\java\seedu\address\logic\commands\CommandTestUtil.java
``` java
    public static final String BIRTHDAY_DESC_AMY = " " + PREFIX_BIRTHDAY + VALID_BIRTHDAY_AMY;
    public static final String BIRTHDAY_DESC_BOB = " " + PREFIX_BIRTHDAY + VALID_BIRTHDAY_BOB;
```
###### \src\test\java\seedu\address\logic\commands\CommandTestUtil.java
``` java
    public static final String EMAIL_DESC_AMY = " " + PREFIX_EMAIL + VALID_EMAIL_AMY;
    public static final String EMAIL_DESC_BOB = " " + PREFIX_EMAIL + VALID_EMAIL_BOB;
    public static final String ADDRESS_DESC_AMY = " " + PREFIX_ADDRESS + VALID_ADDRESS_AMY;
    public static final String ADDRESS_DESC_BOB = " " + PREFIX_ADDRESS + VALID_ADDRESS_BOB;
    public static final String SCORE_DESC_AMY = " " + PREFIX_SCORE + VALID_SCORE_AMY;
    public static final String SCORE_DESC_BOB = " " + PREFIX_SCORE + VALID_SCORE_BOB;
    public static final String TAG_DESC_FRIEND = " " + PREFIX_TAG + VALID_TAG_FRIEND;
    public static final String TAG_DESC_HUSBAND = " " + PREFIX_TAG + VALID_TAG_HUSBAND;

    public static final String INVALID_NAME_DESC = " " + PREFIX_NAME + "James&"; // '&' not allowed in names
    public static final String INVALID_PHONE_DESC = " " + PREFIX_PHONE + "911a"; // 'a' not allowed in phones
```
###### \src\test\java\seedu\address\logic\commands\CommandTestUtil.java
``` java
    // words not allowed for birthday
    public static final String INVALID_BIRTHDAY_DESC = " " + PREFIX_BIRTHDAY + "5/March/1997";
```
###### \src\test\java\seedu\address\logic\commands\CommandTestUtil.java
``` java
    public static final String INVALID_EMAIL_DESC = " " + PREFIX_EMAIL + "bob!yahoo"; // missing '@' symbol
    public static final String INVALID_ADDRESS_DESC = " " + PREFIX_ADDRESS; // empty string not allowed for addresses
    public static final String INVALID_SCORE_DESC = " " + PREFIX_SCORE; // empty string not allowed for score
    public static final String INVALID_TAG_DESC = " " + PREFIX_TAG + "hubby*"; // '*' not allowed in tags

    public static final EditCommand.EditPersonDescriptor DESC_AMY;
    public static final EditCommand.EditPersonDescriptor DESC_BOB;

    static {
```
###### \src\test\java\seedu\address\logic\commands\CommandTestUtil.java
``` java
        DESC_AMY = new EditPersonDescriptorBuilder().withName(VALID_NAME_AMY)
                .withPhone(VALID_PHONE_AMY).withBirthday(VALID_BIRTHDAY_AMY).withEmail(VALID_EMAIL_AMY)
                .withAddress(VALID_ADDRESS_AMY).withScore(VALID_SCORE_AMY).withTags(VALID_TAG_FRIEND).build();
        DESC_BOB = new EditPersonDescriptorBuilder().withName(VALID_NAME_BOB)
                .withPhone(VALID_PHONE_BOB).withBirthday(VALID_BIRTHDAY_AMY).withEmail(VALID_EMAIL_BOB)
                .withAddress(VALID_ADDRESS_BOB).withScore(VALID_SCORE_BOB).withTags(VALID_TAG_HUSBAND,
                        VALID_TAG_FRIEND).build();
```
###### \src\test\java\seedu\address\logic\commands\CommandTestUtil.java
``` java
    }

    /**
     * Executes the given {@code command}, confirms that <br>
     * - the result message matches {@code expectedMessage} <br>
     * - the {@code actualModel} matches {@code expectedModel}
     */
    public static void assertCommandSuccess(Command command, Model actualModel, String expectedMessage,
            Model expectedModel) {
        try {
            CommandResult result = command.execute();
            assertEquals(expectedMessage, result.feedbackToUser);
            assertEquals(expectedModel, actualModel);
        } catch (CommandException ce) {
            throw new AssertionError("Execution of command should not fail.", ce);
        }
    }

    /**
     * Executes the given {@code command}, confirms that <br>
     * - a {@code CommandException} is thrown <br>
     * - the CommandException message matches {@code expectedMessage} <br>
     * - the address book and the filtered person list in the {@code actualModel} remain unchanged
     */
    public static void assertCommandFailure(Command command, Model actualModel, String expectedMessage) {
        // we are unable to defensively copy the model for comparison later, so we can
        // only do so by copying its components.
        AddressBook expectedAddressBook = new AddressBook(actualModel.getAddressBook());
        List<ReadOnlyPerson> expectedFilteredList = new ArrayList<>(actualModel.getFilteredPersonList());

        try {
            command.execute();
            fail("The expected CommandException was not thrown.");
        } catch (CommandException e) {
            assertEquals(expectedMessage, e.getMessage());
            assertEquals(expectedAddressBook, actualModel.getAddressBook());
            assertEquals(expectedFilteredList, actualModel.getFilteredPersonList());
        }
    }

    /**
     * Updates {@code model}'s filtered list to show only the first person in the {@code model}'s address book.
     */
    public static void showFirstPersonOnly(Model model) {
        ReadOnlyPerson person = model.getAddressBook().getPersonList().get(0);
        final String[] splitName = person.getName().fullName.split("\\s+");
        model.updateFilteredPersonList(new NameContainsKeywordsPredicate(Arrays.asList(splitName[0])));

        assert model.getFilteredPersonList().size() == 1;
    }

    /**
     * Updates {@code model}'s favourite filtered list to show only the first person in the {@code model}'s
     * address book.
     */
    public static void showFirstFavouritePersonOnly(Model model) {
        ReadOnlyPerson person = model.getAddressBook().getFavouritePersonList().get(0);
        final String[] splitName = person.getName().fullName.split("\\s+");
        model.updateFilteredFavouritePersonList(new NameContainsKeywordsPredicate(Arrays.asList(splitName[0])));

        assert model.getFilteredFavouritePersonList().size() == 1;
    }

    /**
     * Deletes the first person in {@code model}'s filtered list from {@code model}'s address book.
     */
    public static void deleteFirstPerson(Model model) {
        ReadOnlyPerson firstPerson = model.getFilteredPersonList().get(0);
        try {
            model.deletePerson(firstPerson);
        } catch (PersonNotFoundException pnfe) {
            throw new AssertionError("Person in filtered list must exist in model.", pnfe);
        }
    }
}
```
###### \src\test\java\seedu\address\logic\commands\FavCommandTest.java
``` java
package seedu.address.logic.commands;

import static org.junit.Assert.assertFalse;
import static org.junit.Assert.assertTrue;
import static seedu.address.logic.commands.CommandTestUtil.assertCommandFailure;
import static seedu.address.logic.commands.CommandTestUtil.assertCommandSuccess;
import static seedu.address.logic.commands.CommandTestUtil.showFirstPersonOnly;
import static seedu.address.testutil.TypicalIndexes.INDEX_FIRST_PERSON;
import static seedu.address.testutil.TypicalIndexes.INDEX_SECOND_PERSON;
import static seedu.address.testutil.TypicalPersons.getTypicalAddressBook;

import org.junit.Test;

import seedu.address.commons.core.Messages;
import seedu.address.commons.core.index.Index;
import seedu.address.logic.CommandHistory;
import seedu.address.logic.UndoRedoStack;
import seedu.address.model.Model;
import seedu.address.model.ModelManager;
import seedu.address.model.UserPrefs;
import seedu.address.model.person.ReadOnlyPerson;

/**
 * Contains integration tests (interaction with the Model) and unit tests for {@code FavCommand}.
 */
public class FavCommandTest {

    private Model model = new ModelManager(getTypicalAddressBook(), new UserPrefs());

    @Test
    public void execute_validIndexUnfilteredList_success() throws Exception {
        ReadOnlyPerson personToFav = model.getFilteredPersonList().get(INDEX_FIRST_PERSON.getZeroBased());
        FavCommand favCommand = prepareCommand(INDEX_FIRST_PERSON);

        String expectedMessage = String.format(FavCommand.MESSAGE_FAV_PERSON_SUCCESS, personToFav);

        ModelManager expectedModel = new ModelManager(model.getAddressBook(), new UserPrefs());
        expectedModel.addFavouritePerson(personToFav);

        assertCommandSuccess(favCommand, model, expectedMessage, expectedModel);
    }

    @Test
    public void execute_invalidIndexUnfilteredList_throwsCommandException() throws Exception {
        Index outOfBoundIndex = Index.fromOneBased(model.getFilteredPersonList().size() + 1);
        FavCommand favCommand = prepareCommand(outOfBoundIndex);

        assertCommandFailure(favCommand, model, Messages.MESSAGE_INVALID_PERSON_DISPLAYED_INDEX);
    }

    @Test
    public void execute_validIndexFilteredList_success() throws Exception {
        showFirstPersonOnly(model);

        ReadOnlyPerson personToFav = model.getFilteredPersonList().get(INDEX_FIRST_PERSON.getZeroBased());
        FavCommand favCommand = prepareCommand(INDEX_FIRST_PERSON);

        String expectedMessage = String.format(FavCommand.MESSAGE_FAV_PERSON_SUCCESS, personToFav);

        Model expectedModel = new ModelManager(model.getAddressBook(), new UserPrefs());
        expectedModel.addFavouritePerson(personToFav);

        assertCommandSuccess(favCommand, model, expectedMessage, expectedModel);
    }

    @Test
    public void execute_invalidIndexFilteredList_throwsCommandException() {
        showFirstPersonOnly(model);

        Index outOfBoundIndex = INDEX_SECOND_PERSON;
        // ensures that outOfBoundIndex is still in bounds of address book list
        assertTrue(outOfBoundIndex.getZeroBased() < model.getAddressBook().getPersonList().size());

        FavCommand favCommand = prepareCommand(outOfBoundIndex);

        assertCommandFailure(favCommand, model, Messages.MESSAGE_INVALID_PERSON_DISPLAYED_INDEX);
    }

    @Test
    public void equals() {
        FavCommand favFirstCommand = new FavCommand(INDEX_FIRST_PERSON);
        FavCommand favSecondCommand = new FavCommand(INDEX_SECOND_PERSON);

        // same object -> returns true
        assertTrue(favFirstCommand.equals(favFirstCommand));

        // same values -> returns true
        FavCommand favFirstCommandCopy = new FavCommand(INDEX_FIRST_PERSON);
        assertTrue(favFirstCommand.equals(favFirstCommandCopy));

        // different types -> returns false
        assertFalse(favFirstCommand.equals(1));

        // null -> returns false
        assertFalse(favFirstCommand.equals(null));

        // different person -> returns false
        assertFalse(favFirstCommand.equals(favSecondCommand));
    }

    /**
         * Returns a {@code FavCommand} with the parameter {@code index}.
     */
    private FavCommand prepareCommand(Index index) {
        FavCommand favCommand = new FavCommand(index);
        favCommand.setData(model, new CommandHistory(), new UndoRedoStack());
        return favCommand;
    }
}
```
###### \src\test\java\seedu\address\logic\commands\FavCommandTest.java
``` java

```
###### \src\test\java\seedu\address\logic\commands\FavouriteListCommandTest.java
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

/**
 * Contains integration tests (interaction with the Model) and unit tests for ListCommand.
 */
public class FavouriteListCommandTest {

    private Model model;
    private Model expectedModel;
    private FavouriteListCommand favlistCommand;

    @Before
    public void setUp() {
        model = new ModelManager(getTypicalAddressBook(), new UserPrefs());
        expectedModel = new ModelManager(model.getAddressBook(), new UserPrefs());

        favlistCommand = new FavouriteListCommand();
        favlistCommand.setData(model, new CommandHistory(), new UndoRedoStack());
    }

    @Test
    public void execute_listIsNotFiltered_showsSameList() {
        assertCommandSuccess(favlistCommand, model, FavouriteListCommand.MESSAGE_SUCCESS, expectedModel);
    }

    @Test
    public void execute_listIsFiltered_showsEverything() {
        showFirstPersonOnly(model);
    }
}
```
###### \src\test\java\seedu\address\logic\commands\FavouriteListCommandTest.java
``` java

```
###### \src\test\java\seedu\address\logic\commands\SortCommandTest.java
``` java
package seedu.address.logic.commands;

import static org.junit.Assert.assertFalse;
import static org.junit.Assert.assertTrue;
import static seedu.address.logic.commands.CommandTestUtil.assertCommandSuccess;
import static seedu.address.testutil.TypicalPersons.getTypicalAddressBook;

import org.junit.Test;

import seedu.address.logic.CommandHistory;
import seedu.address.logic.UndoRedoStack;
import seedu.address.model.Model;
import seedu.address.model.ModelManager;
import seedu.address.model.UserPrefs;

/**
 * Contains integration tests (interaction with the Model) for {@code SortCommand}.
 */
public class SortCommandTest {

    final String invalidSortFilter = "random";
    final String sortFilterName = "name";
    final String sortFilterBirthday = "birthday";
    final String sortFilterBirthdayAlias = "b";
    final String sortFilterDefault = "";

    private Model model = new ModelManager(getTypicalAddressBook(), new UserPrefs());

    @Test
    public void execute() throws Exception {

        // Default filter - sort by name
        assertCommandSuccess(prepareCommand(sortFilterDefault), model, SortCommand.MESSAGE_SUCCESS_NAME, model);

        // Sort in alphabhetical order of name
        assertCommandSuccess(prepareCommand(sortFilterName), model, SortCommand.MESSAGE_SUCCESS_NAME, model);

        // Sort in ascending order of birthdays
        assertCommandSuccess(prepareCommand(sortFilterBirthday), model, SortCommand.MESSAGE_SUCCESS_BIRTHDAY, model);

        // Sort in ascending order of birthdays
        assertCommandSuccess(prepareCommand(sortFilterBirthdayAlias), model, SortCommand.MESSAGE_SUCCESS_BIRTHDAY,
                model);
    }

    @Test
    public void equals() {

        final SortCommand sortNameCommand = new SortCommand(sortFilterName);
        final SortCommand sortBirthdayCommand = new SortCommand(sortFilterBirthday);
        final SortCommand sortBirthdayAliasCommand = new SortCommand(sortFilterBirthdayAlias);
        final SortCommand sortDefaultCommand = new SortCommand(sortFilterDefault);

        SortCommand commandExecuted;

        // same filterTypes (Name) -> returns true
        commandExecuted = new SortCommand(sortFilterName);
        assertTrue(sortNameCommand.equals(commandExecuted));

        // same filterTypes (Name) -> returns true
        commandExecuted = new SortCommand(sortFilterBirthday);
        assertTrue(sortBirthdayCommand.equals(commandExecuted));

        // same filterTypes (Name) -> returns true
        commandExecuted = new SortCommand(sortFilterBirthdayAlias);
        assertTrue(sortBirthdayAliasCommand.equals(commandExecuted));

        // same filterTypes (Name) -> returns true
        commandExecuted = new SortCommand(sortFilterDefault);
        assertTrue(sortDefaultCommand.equals(commandExecuted));

        // same object -> returns true
        assertTrue(sortBirthdayCommand.equals(sortBirthdayCommand));

        // null object-> returns false
        assertFalse(sortNameCommand.equals(null));

        // different filterTypes -> returns false
        assertFalse(sortNameCommand.equals(new SortCommand(invalidSortFilter)));

        // different command types -> returns false
        assertFalse(sortDefaultCommand.equals(new UndoCommand()));

    }

    /**
     * Returns a {@code SortCommand} with parameteres.
     */
    private SortCommand prepareCommand(String sortFilter) {
        SortCommand sortCommand = new SortCommand(sortFilter);
        sortCommand.setData(model, new CommandHistory(), new UndoRedoStack());
        return sortCommand;
    }
}
```
###### \src\test\java\seedu\address\logic\commands\SortCommandTest.java
``` java

```
###### \src\test\java\seedu\address\logic\commands\UnfavCommandTest.java
``` java
package seedu.address.logic.commands;

import static org.junit.Assert.assertFalse;
import static org.junit.Assert.assertTrue;
//import static seedu.address.logic.commands.CommandTestUtil.assertCommandSuccess;
import static seedu.address.logic.commands.CommandTestUtil.assertCommandFailure;
import static seedu.address.logic.commands.CommandTestUtil.showFirstPersonOnly;
import static seedu.address.testutil.TypicalIndexes.INDEX_FIRST_PERSON;
import static seedu.address.testutil.TypicalIndexes.INDEX_SECOND_PERSON;
import static seedu.address.testutil.TypicalPersons.getTypicalAddressBook;

import org.junit.Test;

import seedu.address.commons.core.Messages;
import seedu.address.commons.core.index.Index;
import seedu.address.logic.CommandHistory;
import seedu.address.logic.UndoRedoStack;
import seedu.address.model.Model;
import seedu.address.model.ModelManager;
import seedu.address.model.UserPrefs;
//import seedu.address.model.person.ReadOnlyPerson;

/**
 * Contains integration tests (interaction with the Model) and unit tests for {@code UnfavCommand}.
 */
public class UnfavCommandTest {

    private Model model = new ModelManager(getTypicalAddressBook(), new UserPrefs());

    /*
    @Test
    public void execute_validIndexUnfilteredList_success() throws Exception {
        ReadOnlyPerson personToUnfav = model.getFilteredFavouritePersonList().get(INDEX_FIRST_PERSON.getZeroBased());
        UnfavCommand unfavCommand = prepareCommand(INDEX_FIRST_PERSON);

        String expectedMessage = String.format(FavCommand.MESSAGE_FAV_PERSON_SUCCESS, personToUnfav);

        ModelManager expectedModel = new ModelManager(model.getAddressBook(), new UserPrefs());
        expectedModel.removeFavouritePerson(personToUnfav);

        assertCommandSuccess(unfavCommand, model, expectedMessage, expectedModel);
    }
    */
    @Test
    public void execute_invalidIndexUnfilteredList_throwsCommandException() throws Exception {
        Index outOfBoundIndex = Index.fromOneBased(model.getFilteredPersonList().size() + 1);
        UnfavCommand unfavCommand = prepareCommand(outOfBoundIndex);

        assertCommandFailure(unfavCommand, model, Messages.MESSAGE_INVALID_PERSON_DISPLAYED_INDEX);
    }

    /*
    @Test
    public void execute_validIndexFilteredList_success() throws Exception {
        ReadOnlyPerson personToFav = model.getFilteredPersonList().get(INDEX_FIRST_PERSON.getZeroBased());
        FavCommand favCommand = prepareFavCommand(INDEX_FIRST_PERSON);
        Model expectedModel = new ModelManager(model.getAddressBook(), new UserPrefs());
        expectedModel.addFavouritePerson(personToFav);
        showFirstFavouritePersonOnly(model);

        ReadOnlyPerson personToUnfav = model.getFilteredFavouritePersonList().get(INDEX_FIRST_PERSON.getZeroBased());
        UnfavCommand unfavCommand = prepareCommand(INDEX_FIRST_PERSON);

        String expectedMessage = String.format(FavCommand.MESSAGE_FAV_PERSON_SUCCESS, personToUnfav);

        //Model expectedModel = new ModelManager(model.getAddressBook(), new UserPrefs());
        expectedModel.removeFavouritePerson(personToUnfav);
        showNoPerson(expectedModel);

        assertCommandSuccess(unfavCommand, model, expectedMessage, expectedModel);
    }*/

    @Test
    public void execute_invalidIndexFilteredList_throwsCommandException() {
        showFirstPersonOnly(model);

        Index outOfBoundIndex = INDEX_SECOND_PERSON;
        // ensures that outOfBoundIndex is still in bounds of address book list
        assertTrue(outOfBoundIndex.getZeroBased() < model.getAddressBook().getPersonList().size());

        UnfavCommand unfavCommand = prepareCommand(outOfBoundIndex);

        assertCommandFailure(unfavCommand, model, Messages.MESSAGE_INVALID_PERSON_DISPLAYED_INDEX);
    }

    @Test
    public void equals() {
        UnfavCommand unfavFirstCommand = new UnfavCommand(INDEX_FIRST_PERSON);
        UnfavCommand unfavSecondCommand = new UnfavCommand(INDEX_SECOND_PERSON);

        // same object -> returns true
        assertTrue(unfavFirstCommand.equals(unfavFirstCommand));

        // same values -> returns true
        UnfavCommand unfavFirstCommandCopy = new UnfavCommand(INDEX_FIRST_PERSON);
        assertTrue(unfavFirstCommand.equals(unfavFirstCommandCopy));

        // different types -> returns false
        assertFalse(unfavFirstCommand.equals(1));

        // null -> returns false
        assertFalse(unfavFirstCommand.equals(null));

        // different person -> returns false
        assertFalse(unfavFirstCommand.equals(unfavSecondCommand));
    }

    /**
     * Returns a {@code UnfavCommand} with the parameter {@code index}.
     */
    private UnfavCommand prepareCommand(Index index) {
        UnfavCommand unfavCommand = new UnfavCommand(index);
        unfavCommand.setData(model, new CommandHistory(), new UndoRedoStack());
        return unfavCommand;
    }

    /**
     * Updates {@code model}'s filtered list to show no one.
     */
    private void showNoPerson(Model model) {
        model.updateFilteredFavouritePersonList(p -> false);

        assert model.getFilteredFavouritePersonList().isEmpty();
    }

    /**
     * Returns a {@code FavCommand} with the parameter {@code index}.
     */
    private FavCommand prepareFavCommand(Index index) {
        FavCommand favCommand = new FavCommand(index);
        favCommand.setData(model, new CommandHistory(), new UndoRedoStack());
        return favCommand;
    }
}
```
###### \src\test\java\seedu\address\logic\commands\UnfavCommandTest.java
``` java

```
###### \src\test\java\seedu\address\logic\parser\AddCommandParserTest.java
``` java
        Person expectedPerson = new PersonBuilder().withName(VALID_NAME_BOB).withPhone(VALID_PHONE_BOB)
                .withBirthday(VALID_BIRTHDAY_BOB).withEmail(VALID_EMAIL_BOB).withAddress(VALID_ADDRESS_BOB)
                .withScore(VALID_SCORE_BOB).withTags(VALID_TAG_FRIEND).build();
```
###### \src\test\java\seedu\address\logic\parser\AddCommandParserTest.java
``` java

        // multiple names - last name accepted
        assertParseSuccess(parser, AddCommand.COMMAND_WORD + NAME_DESC_AMY + NAME_DESC_BOB + PHONE_DESC_BOB
                + BIRTHDAY_DESC_BOB + EMAIL_DESC_BOB + ADDRESS_DESC_BOB + SCORE_DESC_BOB + TAG_DESC_FRIEND,
                new AddCommand(expectedPerson));

        // multiple phones - last phone accepted
        assertParseSuccess(parser, AddCommand.COMMAND_WORD + NAME_DESC_BOB + PHONE_DESC_AMY + PHONE_DESC_BOB
                + BIRTHDAY_DESC_BOB + EMAIL_DESC_BOB + ADDRESS_DESC_BOB + SCORE_DESC_BOB + TAG_DESC_FRIEND,
                new AddCommand(expectedPerson));

        // multiple emails - last email accepted
        assertParseSuccess(parser, AddCommand.COMMAND_WORD + NAME_DESC_BOB + PHONE_DESC_BOB + BIRTHDAY_DESC_BOB
                + EMAIL_DESC_AMY + EMAIL_DESC_BOB + ADDRESS_DESC_BOB + SCORE_DESC_BOB + TAG_DESC_FRIEND,
                new AddCommand(expectedPerson));

        // multiple addresses - last address accepted
        assertParseSuccess(parser, AddCommand.COMMAND_WORD + NAME_DESC_BOB + PHONE_DESC_BOB + BIRTHDAY_DESC_BOB
                + EMAIL_DESC_BOB + ADDRESS_DESC_AMY + ADDRESS_DESC_BOB + SCORE_DESC_BOB + TAG_DESC_FRIEND,
                new AddCommand(expectedPerson));

        // multiple scores - last score accepted
        //assertParseSuccess(parser, AddCommand.COMMAND_WORD + NAME_DESC_BOB + PHONE_DESC_BOB + EMAIL_DESC_BOB
        //      + ADDRESS_DESC_BOB + SCORE_DESC_AMY + SCORE_DESC_BOB + TAG_DESC_FRIEND,
        //      new AddCommand(expectedPerson));

        // multiple tags - all accepted
        Person expectedPersonMultipleTags = new PersonBuilder().withName(VALID_NAME_BOB).withPhone(VALID_PHONE_BOB)
                .withBirthday(VALID_BIRTHDAY_BOB).withEmail(VALID_EMAIL_BOB).withAddress(VALID_ADDRESS_BOB)
                .withScore(VALID_SCORE_BOB).withTags(VALID_TAG_FRIEND, VALID_TAG_HUSBAND).build();
        assertParseSuccess(parser, AddCommand.COMMAND_WORD + NAME_DESC_BOB + PHONE_DESC_BOB + BIRTHDAY_DESC_BOB
                        + EMAIL_DESC_BOB + ADDRESS_DESC_BOB + SCORE_DESC_BOB + TAG_DESC_HUSBAND + TAG_DESC_FRIEND,
                new AddCommand(expectedPersonMultipleTags));
    }

    @Test
    public void parse_optionalFieldsMissing_success() {
        // zero tags
        Person expectedPerson = new PersonBuilder().withName(VALID_NAME_AMY).withPhone(VALID_PHONE_AMY)
                .withBirthday(VALID_BIRTHDAY_AMY).withEmail(VALID_EMAIL_AMY).withAddress(VALID_ADDRESS_AMY)
                .withScore(VALID_SCORE_AMY).withTags().build();
        assertParseSuccess(parser, AddCommand.COMMAND_WORD + NAME_DESC_AMY + PHONE_DESC_AMY
                + BIRTHDAY_DESC_AMY + EMAIL_DESC_AMY + ADDRESS_DESC_AMY + SCORE_DESC_AMY,
                new AddCommand(expectedPerson));
    }

    @Test
    public void parse_compulsoryFieldMissing_failure() {
        String expectedMessage = String.format(MESSAGE_INVALID_COMMAND_FORMAT, AddCommand.MESSAGE_USAGE);

        // missing name prefix
        assertParseFailure(parser, AddCommand.COMMAND_WORD + VALID_NAME_BOB + PHONE_DESC_BOB
                + EMAIL_DESC_BOB + ADDRESS_DESC_BOB + SCORE_DESC_BOB, expectedMessage);

        // missing phone prefix
        assertParseFailure(parser, AddCommand.COMMAND_WORD + NAME_DESC_BOB + VALID_PHONE_BOB
                + EMAIL_DESC_BOB + ADDRESS_DESC_BOB + SCORE_DESC_BOB, expectedMessage);

        // missing email prefix
        assertParseFailure(parser, AddCommand.COMMAND_WORD + NAME_DESC_BOB + PHONE_DESC_BOB
                + VALID_EMAIL_BOB + ADDRESS_DESC_BOB + SCORE_DESC_BOB, expectedMessage);

        // missing address prefix
        assertParseFailure(parser, AddCommand.COMMAND_WORD + NAME_DESC_BOB + PHONE_DESC_BOB
                + EMAIL_DESC_BOB + VALID_ADDRESS_BOB + SCORE_DESC_BOB, expectedMessage);

        // missing score prefix
        //assertParseFailure(parser, AddCommand.COMMAND_WORD + NAME_DESC_BOB + PHONE_DESC_BOB
        //+ EMAIL_DESC_BOB + ADDRESS_DESC_BOB + VALID_SCORE_BOB, expectedMessage);

        // all prefixes missing
        assertParseFailure(parser, AddCommand.COMMAND_WORD + VALID_NAME_BOB + VALID_PHONE_BOB
                + VALID_EMAIL_BOB + VALID_ADDRESS_BOB + VALID_SCORE_BOB, expectedMessage);
    }

    @Test
    public void parse_invalidValue_failure() {
        // invalid name
        assertParseFailure(parser, AddCommand.COMMAND_WORD + INVALID_NAME_DESC + PHONE_DESC_BOB + BIRTHDAY_DESC_BOB
                + EMAIL_DESC_BOB + ADDRESS_DESC_BOB + SCORE_DESC_BOB + TAG_DESC_HUSBAND + TAG_DESC_FRIEND,
                Name.MESSAGE_NAME_CONSTRAINTS);

        // invalid phone
        assertParseFailure(parser, AddCommand.COMMAND_WORD + NAME_DESC_BOB + INVALID_PHONE_DESC + BIRTHDAY_DESC_BOB
                + EMAIL_DESC_BOB + ADDRESS_DESC_BOB + SCORE_DESC_BOB + TAG_DESC_HUSBAND + TAG_DESC_FRIEND,
                Phone.MESSAGE_PHONE_CONSTRAINTS);

        //invalid birthday
        assertParseFailure(parser, AddCommand.COMMAND_WORD + NAME_DESC_BOB + PHONE_DESC_BOB + INVALID_BIRTHDAY_DESC
                + EMAIL_DESC_BOB + ADDRESS_DESC_BOB + TAG_DESC_HUSBAND + TAG_DESC_FRIEND,
                Birthday.MESSAGE_BIRTHDAY_CONSTRAINTS);

        // invalid email
        assertParseFailure(parser, AddCommand.COMMAND_WORD + NAME_DESC_BOB + PHONE_DESC_BOB + BIRTHDAY_DESC_BOB
                + INVALID_EMAIL_DESC + ADDRESS_DESC_BOB + SCORE_DESC_BOB + TAG_DESC_HUSBAND + TAG_DESC_FRIEND,
                Email.MESSAGE_EMAIL_CONSTRAINTS);

        // invalid address
        assertParseFailure(parser, AddCommand.COMMAND_WORD + NAME_DESC_BOB + PHONE_DESC_BOB + BIRTHDAY_DESC_BOB
                + EMAIL_DESC_BOB + INVALID_ADDRESS_DESC + SCORE_DESC_BOB + TAG_DESC_HUSBAND + TAG_DESC_FRIEND,
                Address.MESSAGE_ADDRESS_CONSTRAINTS);

        // invalid score
        assertParseFailure(parser, AddCommand.COMMAND_WORD + NAME_DESC_BOB + PHONE_DESC_BOB + BIRTHDAY_DESC_BOB
                + EMAIL_DESC_BOB + ADDRESS_DESC_BOB + INVALID_SCORE_DESC + TAG_DESC_HUSBAND + TAG_DESC_FRIEND,
                Score.MESSAGE_SCORE_CONSTRAINTS);

        // invalid tag
        assertParseFailure(parser, AddCommand.COMMAND_WORD + NAME_DESC_BOB + PHONE_DESC_BOB + BIRTHDAY_DESC_BOB
                + EMAIL_DESC_BOB + ADDRESS_DESC_BOB + SCORE_DESC_BOB + INVALID_TAG_DESC + VALID_TAG_FRIEND,
                Tag.MESSAGE_TAG_CONSTRAINTS);

        // two invalid values, only first invalid value reported
        assertParseFailure(parser, AddCommand.COMMAND_WORD + INVALID_NAME_DESC + PHONE_DESC_BOB + BIRTHDAY_DESC_BOB
                + EMAIL_DESC_BOB + INVALID_ADDRESS_DESC + SCORE_DESC_BOB, Name.MESSAGE_NAME_CONSTRAINTS);
    }
}
```
###### \src\test\java\seedu\address\logic\parser\EditCommandParserTest.java
``` java
        //birthday
        userInput = targetIndex.getOneBased() + BIRTHDAY_DESC_AMY;
        descriptor = new EditPersonDescriptorBuilder().withBirthday(VALID_BIRTHDAY_AMY).build();
        expectedCommand = new EditCommand(targetIndex, descriptor);
        assertParseSuccess(parser, userInput, expectedCommand);
```
###### \src\test\java\seedu\address\logic\parser\EditCommandParserTest.java
``` java

        // email
        userInput = targetIndex.getOneBased() + EMAIL_DESC_AMY;
        descriptor = new EditPersonDescriptorBuilder().withEmail(VALID_EMAIL_AMY).build();
        expectedCommand = new EditCommand(targetIndex, descriptor);
        assertParseSuccess(parser, userInput, expectedCommand);

        // address
        userInput = targetIndex.getOneBased() + ADDRESS_DESC_AMY;
        descriptor = new EditPersonDescriptorBuilder().withAddress(VALID_ADDRESS_AMY).build();
        expectedCommand = new EditCommand(targetIndex, descriptor);
        assertParseSuccess(parser, userInput, expectedCommand);

        // score
        userInput = targetIndex.getOneBased() + SCORE_DESC_AMY;
        descriptor = new EditPersonDescriptorBuilder().withScore(VALID_SCORE_AMY).build();
        expectedCommand = new EditCommand(targetIndex, descriptor);
        assertParseSuccess(parser, userInput, expectedCommand);

        // tags
        userInput = targetIndex.getOneBased() + TAG_DESC_FRIEND;
        descriptor = new EditPersonDescriptorBuilder().withTags(VALID_TAG_FRIEND).build();
        expectedCommand = new EditCommand(targetIndex, descriptor);
        assertParseSuccess(parser, userInput, expectedCommand);
    }

    @Test
    public void parse_multipleRepeatedFields_acceptsLast() {
        Index targetIndex = INDEX_FIRST_PERSON;
        String userInput = targetIndex.getOneBased()  + PHONE_DESC_AMY + BIRTHDAY_DESC_AMY + ADDRESS_DESC_AMY
                + EMAIL_DESC_AMY + TAG_DESC_FRIEND + PHONE_DESC_AMY + ADDRESS_DESC_AMY + EMAIL_DESC_AMY
                + TAG_DESC_FRIEND + PHONE_DESC_BOB + ADDRESS_DESC_BOB + EMAIL_DESC_BOB + TAG_DESC_HUSBAND;

        EditPersonDescriptor descriptor = new EditPersonDescriptorBuilder().withPhone(VALID_PHONE_BOB)
                .withBirthday(VALID_BIRTHDAY_AMY).withEmail(VALID_EMAIL_BOB).withAddress(VALID_ADDRESS_BOB)
                .withTags(VALID_TAG_FRIEND, VALID_TAG_HUSBAND).build();
        EditCommand expectedCommand = new EditCommand(targetIndex, descriptor);

        assertParseSuccess(parser, userInput, expectedCommand);
    }

    @Test
    public void parse_invalidValueFollowedByValidValue_success() {
        // no other valid values specified
        Index targetIndex = INDEX_FIRST_PERSON;
        String userInput = targetIndex.getOneBased() + INVALID_PHONE_DESC + PHONE_DESC_BOB;
        EditPersonDescriptor descriptor = new EditPersonDescriptorBuilder().withPhone(VALID_PHONE_BOB).build();
        EditCommand expectedCommand = new EditCommand(targetIndex, descriptor);
        assertParseSuccess(parser, userInput, expectedCommand);

        // other valid values specified
        userInput = targetIndex.getOneBased() + EMAIL_DESC_BOB + INVALID_PHONE_DESC + ADDRESS_DESC_BOB
                + PHONE_DESC_BOB;
        descriptor = new EditPersonDescriptorBuilder().withPhone(VALID_PHONE_BOB).withEmail(VALID_EMAIL_BOB)
                .withAddress(VALID_ADDRESS_BOB).build();
        expectedCommand = new EditCommand(targetIndex, descriptor);
        assertParseSuccess(parser, userInput, expectedCommand);
    }

    @Test
    public void parse_resetTags_success() {
        Index targetIndex = INDEX_THIRD_PERSON;
        String userInput = targetIndex.getOneBased() + TAG_EMPTY;

        EditPersonDescriptor descriptor = new EditPersonDescriptorBuilder().withTags().build();
        EditCommand expectedCommand = new EditCommand(targetIndex, descriptor);

        assertParseSuccess(parser, userInput, expectedCommand);
    }
}
```
###### \src\test\java\seedu\address\logic\parser\FavCommandParserTest.java
``` java
package seedu.address.logic.parser;

import static seedu.address.commons.core.Messages.MESSAGE_INVALID_COMMAND_FORMAT;
import static seedu.address.logic.parser.CommandParserTestUtil.assertParseFailure;
import static seedu.address.logic.parser.CommandParserTestUtil.assertParseSuccess;
import static seedu.address.testutil.TypicalIndexes.INDEX_FIRST_PERSON;
import static seedu.address.testutil.TypicalIndexes.INDEX_SECOND_PERSON;
import static seedu.address.testutil.TypicalIndexes.INDEX_THIRD_PERSON;

import org.junit.Test;

import seedu.address.logic.commands.FavCommand;

/**
 * As we are only doing white-box testing, our test cases do not cover path variations
 * outside of the FavCommand code. For example, inputs "1" and "1 abc" take the
 * same path through the FavCommand, and therefore we test only one of them.
 * The path variation for those two cases occur inside the ParserUtil, and
 * therefore should be covered by the ParserUtilTest.
 */
public class FavCommandParserTest {

    private FavCommandParser parser = new FavCommandParser();

    @Test
    public void parse_validArgs_returnsFavCommand() {
        assertParseSuccess(parser, "1", new FavCommand(INDEX_FIRST_PERSON));
        assertParseSuccess(parser, "2", new FavCommand(INDEX_SECOND_PERSON));
        assertParseSuccess(parser, "3", new FavCommand(INDEX_THIRD_PERSON));
    }

    @Test
    public void parse_invalidArgs_throwsParseException() {

        // Fails when user attempts to add a person into favourite list by character
        assertParseFailure(parser, "a", String.format(MESSAGE_INVALID_COMMAND_FORMAT, FavCommand.MESSAGE_USAGE));

        // Fails when user attempts to add a person into favourite list by name
        assertParseFailure(parser, "Alice", String.format(MESSAGE_INVALID_COMMAND_FORMAT, FavCommand.MESSAGE_USAGE));
    }
}
```
###### \src\test\java\seedu\address\logic\parser\FavCommandParserTest.java
``` java

```
###### \src\test\java\seedu\address\logic\parser\ParserUtilTest.java
``` java
    private static final String INVALID_BIRTHDAY = "1997/05/07 ";
```
###### \src\test\java\seedu\address\logic\parser\ParserUtilTest.java
``` java
    private static final String INVALID_ADDRESS = " ";
    private static final String INVALID_EMAIL = "example.com";
    private static final String INVALID_TAG = "#friend";

    private static final String VALID_NAME = "Rachel Walker";
    private static final String VALID_PHONE = "123456";
```
###### \src\test\java\seedu\address\logic\parser\ParserUtilTest.java
``` java
    private static final String VALID_BIRTHDAY = "17/07/2006";
```
###### \src\test\java\seedu\address\logic\parser\ParserUtilTest.java
``` java
    private static final String VALID_ADDRESS = "123 Main Street #0505";
    private static final String VALID_EMAIL = "rachel@example.com";
    private static final String VALID_TAG_1 = "friend";
    private static final String VALID_TAG_2 = "neighbour";

    @Rule
    public final ExpectedException thrown = ExpectedException.none();

    @Test
    public void parseIndex_invalidInput_throwsIllegalValueException() throws Exception {
        thrown.expect(IllegalValueException.class);
        ParserUtil.parseIndex("10 a");
    }

    @Test
    public void parseIndex_outOfRangeInput_throwsIllegalValueException() throws Exception {
        thrown.expect(IllegalValueException.class);
        thrown.expectMessage(MESSAGE_INVALID_INDEX);
        ParserUtil.parseIndex(Long.toString(Integer.MAX_VALUE + 1));
    }

    @Test
    public void parseIndex_validInput_success() throws Exception {
        // No whitespaces
        assertEquals(INDEX_FIRST_PERSON, ParserUtil.parseIndex("1"));

        // Leading and trailing whitespaces
        assertEquals(INDEX_FIRST_PERSON, ParserUtil.parseIndex("  1  "));
    }

    @Test
    public void parseName_null_throwsNullPointerException() throws Exception {
        thrown.expect(NullPointerException.class);
        ParserUtil.parseName(null);
    }

    @Test
    public void parseName_invalidValue_throwsIllegalValueException() throws Exception {
        thrown.expect(IllegalValueException.class);
        ParserUtil.parseName(Optional.of(INVALID_NAME));
    }

    @Test
    public void parseName_optionalEmpty_returnsOptionalEmpty() throws Exception {
        assertFalse(ParserUtil.parseName(Optional.empty()).isPresent());
    }

    @Test
    public void parseName_validValue_returnsName() throws Exception {
        Name expectedName = new Name(VALID_NAME);
        Optional<Name> actualName = ParserUtil.parseName(Optional.of(VALID_NAME));

        assertEquals(expectedName, actualName.get());
    }

    @Test
    public void parsePhone_null_throwsNullPointerException() throws Exception {
        thrown.expect(NullPointerException.class);
        ParserUtil.parsePhone(null);
    }

    @Test
    public void parsePhone_invalidValue_throwsIllegalValueException() throws Exception {
        thrown.expect(IllegalValueException.class);
        ParserUtil.parsePhone(Optional.of(INVALID_PHONE));
    }

    @Test
    public void parsePhone_optionalEmpty_returnsOptionalEmpty() throws Exception {
        assertFalse(ParserUtil.parsePhone(Optional.empty()).isPresent());
    }

    @Test
    public void parsePhone_validValue_returnsPhone() throws Exception {
        Phone expectedPhone = new Phone(VALID_PHONE);
        Optional<Phone> actualPhone = ParserUtil.parsePhone(Optional.of(VALID_PHONE));

        assertEquals(expectedPhone, actualPhone.get());
    }

```
###### \src\test\java\seedu\address\logic\parser\ParserUtilTest.java
``` java
    @Test
    public void parseBirthday_null_throwsNullPointerException() throws Exception {
        thrown.expect(NullPointerException.class);
        ParserUtil.parseBirthday(null);
    }

    @Test
    public void parseBirthday_invalidValue_throwsIllegalValueException() throws Exception {
        thrown.expect(IllegalValueException.class);
        ParserUtil.parseBirthday(Optional.of(INVALID_BIRTHDAY));
    }

    @Test
    public void parseBirthday_optionalEmpty_returnsOptionalEmpty() throws Exception {
        //assertFalse(ParserUtil.parseBirthday(Optional.empty()).isPresent());
    }

    @Test
    public void parseBirthday_validValue_returnsBirthday() throws Exception {
        Birthday expectedBirthday = new Birthday(VALID_BIRTHDAY);
        Optional<Birthday> actualBirthday = ParserUtil.parseBirthday(Optional.of(VALID_BIRTHDAY));
        assertEquals(expectedBirthday, actualBirthday.get());
    }
```
###### \src\test\java\seedu\address\logic\parser\ParserUtilTest.java
``` java

    @Test
    public void parseAddress_null_throwsNullPointerException() throws Exception {
        thrown.expect(NullPointerException.class);
        ParserUtil.parseAddress(null);
    }

    @Test
    public void parseAddress_invalidValue_throwsIllegalValueException() throws Exception {
        thrown.expect(IllegalValueException.class);
        ParserUtil.parseAddress(Optional.of(INVALID_ADDRESS));
    }

    @Test
    public void parseAddress_optionalEmpty_returnsOptionalEmpty() throws Exception {
        assertFalse(ParserUtil.parseAddress(Optional.empty()).isPresent());
    }

    @Test
    public void parseAddress_validValue_returnsAddress() throws Exception {
        Address expectedAddress = new Address(VALID_ADDRESS);
        Optional<Address> actualAddress = ParserUtil.parseAddress(Optional.of(VALID_ADDRESS));

        assertEquals(expectedAddress, actualAddress.get());
    }

    @Test
    public void parseEmail_null_throwsNullPointerException() throws Exception {
        thrown.expect(NullPointerException.class);
        ParserUtil.parseEmail(null);
    }

    @Test
    public void parseEmail_invalidValue_throwsIllegalValueException() throws Exception {
        thrown.expect(IllegalValueException.class);
        ParserUtil.parseEmail(Optional.of(INVALID_EMAIL));
    }

    @Test
    public void parseEmail_optionalEmpty_returnsOptionalEmpty() throws Exception {
        assertFalse(ParserUtil.parseEmail(Optional.empty()).isPresent());
    }

    @Test
    public void parseEmail_validValue_returnsEmail() throws Exception {
        Email expectedEmail = new Email(VALID_EMAIL);
        Optional<Email> actualEmail = ParserUtil.parseEmail(Optional.of(VALID_EMAIL));

        assertEquals(expectedEmail, actualEmail.get());
    }

    @Test
    public void parseTags_null_throwsNullPointerException() throws Exception {
        thrown.expect(NullPointerException.class);
        ParserUtil.parseTags(null);
    }

    @Test
    public void parseTags_collectionWithInvalidTags_throwsIllegalValueException() throws Exception {
        thrown.expect(IllegalValueException.class);
        ParserUtil.parseTags(Arrays.asList(VALID_TAG_1, INVALID_TAG));
    }

    @Test
    public void parseTags_emptyCollection_returnsEmptySet() throws Exception {
        assertTrue(ParserUtil.parseTags(Collections.emptyList()).isEmpty());
    }

    @Test
    public void parseTags_collectionWithValidTags_returnsTagSet() throws Exception {
        Set<Tag> actualTagSet = ParserUtil.parseTags(Arrays.asList(VALID_TAG_1, VALID_TAG_2));
        Set<Tag> expectedTagSet = new HashSet<Tag>(Arrays.asList(new Tag(VALID_TAG_1), new Tag(VALID_TAG_2)));

        assertEquals(expectedTagSet, actualTagSet);
    }
}
```
###### \src\test\java\seedu\address\logic\parser\SortCommandParserTest.java
``` java
package seedu.address.logic.parser;

import static seedu.address.commons.core.Messages.MESSAGE_INVALID_COMMAND_FORMAT;
import static seedu.address.logic.parser.CommandParserTestUtil.assertParseFailure;
import static seedu.address.logic.parser.CommandParserTestUtil.assertParseSuccess;

import org.junit.Test;

import seedu.address.logic.commands.SortCommand;

public class SortCommandParserTest {

    final String invalidSortFilter = "people";
    final String sortFilterBirthday = "birthday";
    final String sortFilterBirthdayAlias = "b";
    final String sortFilterDefault = "";
    final String sortFilterName = "name";

    private SortCommandParser parser = new SortCommandParser();

    @Test
    public void parse_validArgs_returnsSortCommand() throws Exception {

        String userInput;
        SortCommand expectedCommand;

        // No sortFilter argument: default sort in alphabhetical order of names
        userInput = SortCommand.COMMAND_WORD + sortFilterDefault;
        expectedCommand = new SortCommand(sortFilterDefault);
        assertParseSuccess(parser, userInput, expectedCommand);

        // Sorting in alphabhetical order of names
        userInput = SortCommand.COMMAND_WORD + " " + sortFilterName;
        expectedCommand = new SortCommand(sortFilterName);
        assertParseSuccess(parser, userInput, expectedCommand);

        // Sorting in ascending order of birthdays
        userInput = SortCommand.COMMAND_WORD + " " + sortFilterBirthday;
        expectedCommand = new SortCommand(sortFilterBirthday);
        assertParseSuccess(parser, userInput, expectedCommand);

        // Sorting in ascending order of birthdays using alias 'b' for birthdays
        userInput = SortCommand.COMMAND_WORD + " " + sortFilterBirthdayAlias;
        expectedCommand = new SortCommand(sortFilterBirthdayAlias);
        assertParseSuccess(parser, userInput, expectedCommand);

        // Sorting in alphabhetical order of names with extra spaces
        userInput = SortCommand.COMMAND_WORD + "     " + sortFilterName;
        expectedCommand = new SortCommand(sortFilterName);
        assertParseSuccess(parser, userInput, expectedCommand);

    }

    @Test
    public void parse_invalid_arguments() throws Exception {
        String userInput = SortCommand.COMMAND_WORD + " " + invalidSortFilter;
        String expectedMessage = String.format(MESSAGE_INVALID_COMMAND_FORMAT, SortCommand.MESSAGE_USAGE);
        assertParseFailure(parser, userInput, expectedMessage);
    }
}
```
###### \src\test\java\seedu\address\logic\parser\SortCommandParserTest.java
``` java

```
###### \src\test\java\seedu\address\logic\parser\UnfavCommandParserTest.java
``` java
package seedu.address.logic.parser;

import static seedu.address.commons.core.Messages.MESSAGE_INVALID_COMMAND_FORMAT;
import static seedu.address.logic.parser.CommandParserTestUtil.assertParseFailure;
import static seedu.address.logic.parser.CommandParserTestUtil.assertParseSuccess;
import static seedu.address.testutil.TypicalIndexes.INDEX_FIRST_PERSON;
import static seedu.address.testutil.TypicalIndexes.INDEX_SECOND_PERSON;
import static seedu.address.testutil.TypicalIndexes.INDEX_THIRD_PERSON;

import org.junit.Test;

import seedu.address.logic.commands.UnfavCommand;

/**
 * As we are only doing white-box testing, our test cases do not cover path variations
 * outside of the UnfavCommand code. For example, inputs "1" and "1 abc" take the
 * same path through the UnfavCommand, and therefore we test only one of them.
 * The path variation for those two cases occur inside the ParserUtil, and
 * therefore should be covered by the ParserUtilTest.
 */
public class UnfavCommandParserTest {

    private UnfavCommandParser parser = new UnfavCommandParser();

    @Test
    public void parse_validArgs_returnsFavCommand() {
        assertParseSuccess(parser, "1", new UnfavCommand(INDEX_FIRST_PERSON));
        assertParseSuccess(parser, "2", new UnfavCommand(INDEX_SECOND_PERSON));
        assertParseSuccess(parser, "3", new UnfavCommand(INDEX_THIRD_PERSON));
    }

    @Test
    public void parse_invalidArgs_throwsParseException() {

        // Fails when user attempts to remove a person from favourite list by character
        assertParseFailure(parser, "a", String.format(MESSAGE_INVALID_COMMAND_FORMAT, UnfavCommand.MESSAGE_USAGE));

        // Fails when user attempts to remove a person from favourite list by name
        assertParseFailure(parser, "Alice", String.format(MESSAGE_INVALID_COMMAND_FORMAT, UnfavCommand.MESSAGE_USAGE));
    }
}
```
###### \src\test\java\seedu\address\logic\parser\UnfavCommandParserTest.java
``` java

```
###### \src\test\java\seedu\address\model\person\BirthdayTest.java
``` java
package seedu.address.model.person;

import static org.junit.Assert.assertFalse;
import static org.junit.Assert.assertTrue;

import org.junit.Test;

public class BirthdayTest {

    @Test
    public void isValidBirthday() {

        // valid birthdays
        assertTrue(Birthday.isValidBirthday("11/01/1999"));
        assertTrue(Birthday.isValidBirthday("16/08/1968"));
        assertTrue(Birthday.isValidBirthday("21/04/1973"));
        assertTrue(Birthday.isValidBirthday("17/06/2006"));

        // invalid birthdays
        assertFalse(Birthday.isValidBirthday("")); // empty
        assertFalse(Birthday.isValidBirthday(" ")); // only space
        assertFalse(Birthday.isValidBirthday("1999/01  /11")); // extra space
        assertFalse(Birthday.isValidBirthday("1999/01/11")); // wrong format
        assertFalse(Birthday.isValidBirthday("11/January/1999")); // non-numeric
        assertFalse(Birthday.isValidBirthday("01.02#99")); // non-numeric characters
        assertFalse(Birthday.isValidBirthday("11/02/19899")); // invalid year
        assertFalse(Birthday.isValidBirthday("01/022/1973")); // invalid month
        assertFalse(Birthday.isValidBirthday("40/05/1998")); // invalid date
        assertFalse(Birthday.isValidBirthday("29/02/1989")); // invalid date(non-leap year does not have 29th Feb)

    }
}
```
###### \src\test\java\seedu\address\model\person\BirthdayTest.java
``` java

```
###### \src\test\java\seedu\address\testutil\EditPersonDescriptorBuilder.java
``` java
    /**
     * Sets the {@code Birthday} of the {@code EditPersonDescriptor} that we are building.
     */
    public EditPersonDescriptorBuilder withBirthday(String birthday) {
        try {
            ParserUtil.parseBirthday(Optional.of(birthday)).ifPresent(descriptor::setBirthday);
        } catch (IllegalValueException ive) {
            throw new IllegalArgumentException("birthday is expected to be unique.");
        }
        return this;
    }
```
###### \src\test\java\seedu\address\testutil\EditPersonDescriptorBuilder.java
``` java

    /**
     * Sets the {@code Email} of the {@code EditPersonDescriptor} that we are building.
     */
    public EditPersonDescriptorBuilder withEmail(String email) {
        try {
            ParserUtil.parseEmail(Optional.of(email)).ifPresent(descriptor::setEmail);
        } catch (IllegalValueException ive) {
            throw new IllegalArgumentException("email is expected to be unique.");
        }
        return this;
    }

    /**
     * Sets the {@code Address} of the {@code EditPersonDescriptor} that we are building.
     */
    public EditPersonDescriptorBuilder withAddress(String address) {
        try {
            ParserUtil.parseAddress(Optional.of(address)).ifPresent(descriptor::setAddress);
        } catch (IllegalValueException ive) {
            throw new IllegalArgumentException("address is expected to be unique.");
        }
        return this;
    }

    /**
     * Sets the {@code Score} of the {@code EditPersonDescriptor} that we are building.
     */
    public EditPersonDescriptorBuilder withScore(String score) {
        try {
            ParserUtil.parseScore(Optional.of(score)).ifPresent(descriptor::setScore);
        } catch (IllegalValueException ive) {
            throw new IllegalArgumentException("score is expected to be unique");
        }
        return this;
    }

    /**
     * Parses the {@code tags} into a {@code Set<Tag>} and set it to the {@code EditPersonDescriptor}
     * that we are building.
     */
    public EditPersonDescriptorBuilder withTags(String... tags) {
        try {
            descriptor.setTags(ParserUtil.parseTags(Arrays.asList(tags)));
        } catch (IllegalValueException ive) {
            throw new IllegalArgumentException("tags are expected to be unique.");
        }
        return this;
    }

    public EditPersonDescriptor build() {
        return descriptor;
    }
}
```
###### \src\test\java\seedu\address\testutil\PersonBuilder.java
``` java
    public static final String DEFAULT_BIRTHDAY = "11/01/1999";
```
###### \src\test\java\seedu\address\testutil\PersonBuilder.java
``` java
    public static final String DEFAULT_EMAIL = "alice@gmail.com";
    public static final String DEFAULT_ADDRESS = "123, Jurong West Ave 6, #08-111";
    public static final String DEFAULT_SCORE = "7";
    public static final String DEFAULT_TAGS = "friends";

    private Person person;

    public PersonBuilder() {
        try {
            Name defaultName = new Name(DEFAULT_NAME);
            Phone defaultPhone = new Phone(DEFAULT_PHONE);
```
###### \src\test\java\seedu\address\testutil\PersonBuilder.java
``` java
            Birthday defaultBirthday = new Birthday(DEFAULT_BIRTHDAY);
```
###### \src\test\java\seedu\address\testutil\PersonBuilder.java
``` java
            Email defaultEmail = new Email(DEFAULT_EMAIL);
            Address defaultAddress = new Address(DEFAULT_ADDRESS);
            Score defaultScore = new Score(DEFAULT_SCORE);
            Set<Tag> defaultTags = SampleDataUtil.getTagSet(DEFAULT_TAGS);
            this.person = new Person(defaultName, defaultPhone, defaultBirthday, defaultEmail, defaultAddress,
                    defaultScore, defaultTags);
        } catch (IllegalValueException ive) {
            throw new AssertionError("Default person's values are invalid.");
        }
    }

    /**
     * Initializes the PersonBuilder with the data of {@code personToCopy}.
     */
    public PersonBuilder(ReadOnlyPerson personToCopy) {
        this.person = new Person(personToCopy);
    }

    /**
     * Sets the {@code Name} of the {@code Person} that we are building.
     */
    public PersonBuilder withName(String name) {
        try {
            this.person.setName(new Name(name));
        } catch (IllegalValueException ive) {
            throw new IllegalArgumentException("name is expected to be unique.");
        }
        return this;
    }

    /**
     * Parses the {@code tags} into a {@code Set<Tag>} and set it to the {@code Person} that we are building.
     */
    public PersonBuilder withTags(String ... tags) {
        try {
            this.person.setTags(SampleDataUtil.getTagSet(tags));
        } catch (IllegalValueException ive) {
            throw new IllegalArgumentException("tags are expected to be unique.");
        }
        return this;
    }

    /**
     * Sets the {@code Address} of the {@code Person} that we are building.
     */
    public PersonBuilder withAddress(String address) {
        try {
            this.person.setAddress(new Address(address));
        } catch (IllegalValueException ive) {
            throw new IllegalArgumentException("address is expected to be unique.");
        }
        return this;
    }

    /**
     * Sets the {@code Phone} of the {@code Person} that we are building.
     */
    public PersonBuilder withPhone(String phone) {
        try {
            this.person.setPhone(new Phone(phone));
        } catch (IllegalValueException ive) {
            throw new IllegalArgumentException("phone is expected to be unique.");
        }
        return this;
    }

```
###### \src\test\java\seedu\address\testutil\PersonBuilder.java
``` java
    /**
     * Sets the {@code Birthday} of the {@code Person} that we are building.
     */
    public PersonBuilder withBirthday(String birthday) {
        try {
            this.person.setBirthday(new Birthday(birthday));
        } catch (IllegalValueException ive) {
            throw new IllegalArgumentException("birthday is expected to be unique.");
        }
        return this;
    }
```
###### \src\test\java\seedu\address\testutil\PersonBuilder.java
``` java

    /**
     * Sets the {@code Email} of the {@code Person} that we are building.
     */
    public PersonBuilder withEmail(String email) {
        try {
            this.person.setEmail(new Email(email));
        } catch (IllegalValueException ive) {
            throw new IllegalArgumentException("email is expected to be unique.");
        }
        return this;
    }

    /**
     *Sets the {@code Score} of the {@code Person} that we are building.
     */
    public PersonBuilder withScore(String score) {
        try {
            this.person.setScore(new Score(score));
        } catch (IllegalValueException ive) {
            throw new IllegalArgumentException("score is expected to be unique");
        }
        return this;
    }

    public Person build() {
        return this.person;
    }

}
```
###### \src\test\java\seedu\address\ui\testutil\GuiTestAssert.java
``` java
        assertEquals(expectedPerson.getBirthday().value, actualCard.getBirthday());
```
###### \src\test\java\seedu\address\ui\testutil\GuiTestAssert.java
``` java
        assertEquals(expectedPerson.getEmail().value, actualCard.getEmail());
        assertEquals(expectedPerson.getAddress().value, actualCard.getAddress());
        assertEquals(expectedPerson.getTags().stream().map(tag -> tag.tagName).collect(Collectors.toList()),
                actualCard.getTags());
    }

    /**
     * Asserts that the list in {@code personListPanelHandle} displays the details of {@code persons} correctly and
     * in the correct order.
     */
    public static void assertListMatching(PersonListPanelHandle personListPanelHandle, ReadOnlyPerson... persons) {
        for (int i = 0; i < persons.length; i++) {
            assertCardDisplaysPerson(persons[i], personListPanelHandle.getPersonCardHandle(i));
        }
    }

    /**
     * Asserts that the list in {@code personListPanelHandle} displays the details of {@code persons} correctly and
     * in the correct order.
     */
    public static void assertListMatching(PersonListPanelHandle personListPanelHandle, List<ReadOnlyPerson> persons) {
        assertListMatching(personListPanelHandle, persons.toArray(new ReadOnlyPerson[0]));
    }

    /**
     * Asserts the size of the list in {@code personListPanelHandle} equals to {@code size}.
     */
    public static void assertListSize(PersonListPanelHandle personListPanelHandle, int size) {
        int numberOfPeople = personListPanelHandle.getListSize();
        assertEquals(size, numberOfPeople);
    }

    /**
     * Asserts the message shown in {@code resultDisplayHandle} equals to {@code expected}.
     */
    public static void assertResultMessage(ResultDisplayHandle resultDisplayHandle, String expected) {
        assertEquals(expected, resultDisplayHandle.getText());
    }
}
```
