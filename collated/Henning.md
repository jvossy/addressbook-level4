# Henning
###### \out\production\resources\view\PersonListCard.fxml
``` fxml
      <Label fx:id="score" styleClass="cell_small_label"  text="\$score" />
```
###### \src\main\java\seedu\address\logic\parser\ParserUtil.java
``` java
    public static Optional<Score> parseScore(Optional<String> score) throws IllegalValueException {
        requireNonNull(score);
        return score.isPresent() ? Optional.of(new Score(score.get())) : Optional.of(new Score(""));
    }
```
###### \src\main\java\seedu\address\model\person\Person.java
``` java
    public void setScore(Score score) {
        this.score.set(requireNonNull(score));
    }

    @Override
    public ObjectProperty<Score> scoreProperty() {
        return score;
    }

    @Override
    public Score getScore() {
        return score.get();
    }

```
###### \src\main\java\seedu\address\model\person\ReadOnlyPerson.java
``` java
                .append(" ")
                .append(getScore())
```
###### \src\main\java\seedu\address\model\person\Score.java
``` java
import static java.util.Objects.requireNonNull;

import seedu.address.commons.exceptions.IllegalValueException;

/**
 * Represents a persons score in the address book.
 * Guarantees: immutable; is valid.
 */
public class Score {

    public static final String MESSAGE_SCORE_CONSTRAINTS =
            "The score should be a number between 0 and 9, with 9 being the best score and 0 the worst.";

    public static final String SCORE_VALIDATION_REGEX = "\\d";
    public final String value;

    public Score(String score) throws IllegalValueException {
        requireNonNull(score);
        if (score.equals("")) {
            this.value = score;
        } else {
            String filteredScore = score.replaceAll("[^\\d]", "");
            if (!isValidScore(filteredScore)) {
                throw new IllegalValueException(MESSAGE_SCORE_CONSTRAINTS);
            }
            this.value = "Group score: " + filteredScore;
        }
    }

    public boolean isValidScore(String value) {
        return value.matches(SCORE_VALIDATION_REGEX);
    }

    @Override
    public String toString() {
        return value;
    }


    @Override
    public boolean equals(Object other) {
        return other == this || (other instanceof Score && this.value.equals(((Score) other).value));
    }

    @Override
    public int hashCode() {
        return value.hashCode();
    }
}
```
###### \src\main\resources\view\PersonListCard.fxml
``` fxml
      <Label fx:id="score" styleClass="cell_small_label"  text="\$score" />
```
