# Ruby String

Go beyond "Hello, world" and unlock the full power of Ruby's String class.

## Goal

In this lesson, you'll learn how to work with text (strings) in Ruby: creating them, manipulating them, taking input, searching with regular expressions, understanding encodings, and more.

## What is a String?

In programming, a string is a data type used to represent *text* rather than *numbers*. It is a sequence of characters that can include letters, numbers, symbols, and spaces, and must be enclosed in quotation marks (`"` or `'`).

For example, `"hello"`, `"123"`, and `":)"` are all valid strings.

```ruby
pp "hello"
pp "123"
pp ":)"
```
{: .repl }

## 1. Creating Strings

You can create strings with double quotes (`"`) or single quotes (`'`).

```ruby
greeting = "Hello, world!"
pp greeting

farewell = 'Goodbye!'
pp farewell
```
{: .repl }

## 2. Combining Strings

### Concatenation

Strings can be combined with the `concat` method, this is called *concatenation*. [docs](https://ruby-doc.org/3.4.1/String.html#method-i-concat)

```ruby
first = "Hello"
second = "World"
first.concat(" ", second)

pp first
```
{: .repl }

Use `+` to concatenate strings without changing (mutating) the receiver. [docs](https://ruby-doc.org/3.4.1/String.html#method-i-2B)

```ruby
first = "Hello"
second = "World"
pp first + " " + second
pp first
```
{: .repl }

### Interpolation

*Interpolation* lets you insert variables directly inside double-quoted (`""`) strings. Notice in this example how we use the hash symbol (`#`) and curly braces (`{}`) to inject the name variable into the string.

```ruby
name = "Ruby"
puts "Hello, #{name}!"
```
{: .repl }

<aside class="warning">
  <strong>Note:</strong> Interpolation works only with double quotes <code>"</code>, not single quotes <code>'</code>.
</aside>

## 3. String Math

A key characteristic of strings is they are treated as text, not numerical values; for instance, the string `"1"` is different from the number `1`, and adding two strings like `"1" + "2"` results in the concatenated string `"12"` rather than the number `3`.

```ruby
pp "1" + "2"
```
{: .repl }

Use `*` to make copies of a string. [docs](https://ruby-doc.org/3.4.1/String.html#method-i-2A)

```ruby
pp "hello" * 3
```
{: .repl }

## 4. User Input

Ruby's `gets` method reads user input. [docs](https://ruby-doc.org/3.4.1/exts/stringio/StringIO.html#method-i-gets)

<!-- FIXME: this wont work in online repl. or add screenshot video -->
```ruby
print "What is your name? "
name = gets
puts "Hello, #{name}!"
```

```ruby
# Output (when user enters Alice):
Hello, Alice\n
!
```

When using the `gets` method in Ruby to read user input, the newline character (`\n`) is included at the end of the string because it is part of the input stream that the user generates when pressing the Enter key. This newline character is not part of the text the user typed but is added by the terminal when the user finishes their input. As a result, if you try to compare the string directly with another string, the comparison might fail due to the presence of this extra `\n` character. The best way to remove this extra newline character is to use the `chomp` method.

```ruby
print "What is your name? "
name = gets.chomp
puts "Hello, #{name}!"
```

```ruby
# Output (when user enters Alice):
Hello, Alice!
```

<aside class="tip">
  Combining <code>gets</code> and <code>chomp</code> methods happense so frequently that <code>gets</code> allows you to pass an argument to automatically chomp the input. <code>gets(chomp: true)</code> will remove the extra newline for you.
</aside>

## 5. Common String Methods

There are a handful of common String methods that you should be familiar with. Don't worry about memorizing all these methods. (nobody has them all memorized) Get familiar with what is available and reach for these methods when the moment arises. Remember, you can always consult the [docs](https://ruby-doc.org/).

### strip

Remove leading and trailing whitespace. [docs](https://ruby-doc.org/3.4.1/String.html#method-i-strip)

```ruby
word = " hello "
pp word.strip       # "hello"
```
{: .repl }

### upcase

Convert lowercase characters to uppercase. [docs](https://ruby-doc.org/3.4.1/String.html#method-i-upcase)

```ruby
word = "hello"
pp word.upcase      # "HELLO"
```
{: .repl }

### downcase

Convert uppercase characters to lowercase. [docs](https://ruby-doc.org/3.4.1/String.html#method-i-downcase)

```ruby
word = "HELLO"
pp word.downcase    # "hello"
```
{: .repl }

### capitalize

Convert the first character in a string to uppercase. [docs](https://ruby-doc.org/3.4.1/String.html#method-i-capitalize)

```ruby
word = "hello"
pp word.capitalize  # "Hello"
```
{: .repl }

### reverse

Reverse the order of characters in a string. [docs](https://ruby-doc.org/3.4.1/String.html#method-i-reverse)

```ruby
word = "hello"
pp word.reverse     # "olleh"
```
{: .repl }

### length

Get the count of characters in a string. [docs](https://ruby-doc.org/3.4.1/String.html#method-i-length)

```ruby
word = "hello"
pp word.length      # 5
```
{: .repl }

### chars

Convert the string into an array of characters. [docs](https://ruby-doc.org/3.4.1/String.html#method-i-chars)

```ruby
word = "hello"
pp word.chars      # ["h", "e", "l", "l", "o"]
```

### Ruby Convention on `!` Operator Methods

In Ruby, the exclamation mark (!) is a naming convention used for methods that perform a destructive operation or have side effects, meaning they alter the object's state or perform a potentially dangerous action.

For example, `String#upcase!` modifies the string in place, while `String#upcase` returns a new string with the uppercase version, leaving the original unchanged.

```ruby
word = "hello"
pp word.upcase
pp word
pp word.upcase!
pp word
```
{: .repl }

## 6. Indexing and Slices

Strings work like lists of characters.

![array of charaters](https://upload.wikimedia.org/wikipedia/commons/6/6b/String_example.png)

You can access single characters or slices using `String#slice`. [docs](https://ruby-doc.org/3.4.1/String.html#method-i-slice)

`String#slice` method accepts either an integer or [range](https://docs.ruby-lang.org/en/master/Range.html) of integers.

```ruby
text = "Ruby"

pp text.slice(0)     # "R"
pp text.slice(1..2)  # "ub"
pp text.slice(-1)    # "y"
```
{: .repl }

## 7. Substitution with `gsub` and Regular Expressions

`String#gsub` replaces text. [docs](https://ruby-doc.org/3.4.1/String.html#method-i-gsub)

```ruby
phrase = "I have 3 cats."

pp phrase.gsub("cats", "dogs")
```
{: .repl }

With regular expressions (regex for short), it becomes even more powerful. Regular expressions are declared inside forward slashes (`/`). Here are some example regular expressions.

```ruby
phrase = "I have 3 cats."


pp phrase.gsub(/\d/, "#")          # Replace digits
pp phrase.gsub(/cats?/, "birds")   # Replace "cat" or "cats"
pp phrase.gsub(/[aeiou]/, '*')     # Replace vowels with *
pp phrase.gsub(/^[aeiou]/, '*')    # Replace non-vowels with *
```
{: .repl }

Regular expressions are notoriously unintuitive. It's worth learning a few of the basics as they show up a lot in coding interview questions. Be on the lookout for problems where a regular expression provides an elegant solution to a problem.

### Interactive Regular Expression Tools

Regex can feel abstract until you test it. These tools let you write regex and instantly see matches:

- [RegExr](https://regexr.com/)
- [Regex101](https://regex101.com/)
- [RegexOne](https://regexone.com/)

## 8. Character Codes and Encoding

<!-- computers think in 1s and 0s, humans think more using written word -->

Under the hood, strings are sequences of bytes with an encoding (UTF-8 by default). Every character has an underlying integer value. See [ascii-code.com](https://www.ascii-code.com/) for a ascii code chart.

```ruby
pp "Ruby".encoding    # UTF-8
pp "A".ord            # 65 (ASCII code for 'A')
pp 65.chr             # "A"
```
{: .repl }

## 9. Mutability and `freeze`

Strings in Ruby are *mutable* (you can change them).

```ruby
s = "Hi"
s << " there"
pp s   # "Hi there"
```
{: .repl }

You can make a string *immutable* (you can't change it) using the `freeze` method. This can be helpful for data integrity, ensuring we don't accidentally change string values we shouldn't.

```ruby
name = "Bob".freeze
name << "by"   # Raises FrozenError
```
{: .repl }

## 10. String Comparison

Use `String#eql?` to compare 2 strings for length and content. [docs](https://ruby-doc.org/3.4.1/String.html#method-i-eql-3F)

```ruby
pp "apple".eql?("Apple")    # false
pp "apple".eql?("apple")    # true

# Each char has a corresponding integer value on the ascii chart
pp "a" < "b"                # true (alphabetical)
```
{: .repl }

### Ruby Convention on ? Operator Methods

In Ruby, the question mark (?) at the end of a method name is a convention that signals the method will return a Boolean value (true or false). These are sometimes called predicate methods, because they answer a yes/no question about the object.

For example, `String#empty?` checks if a string has no characters, while `String#start_with?` checks if a string begins with a given substring.

```ruby
word = "hello"

pp word.empty?             # => false
pp word.start_with?("he")  # => true
pp word.include?("z")      # => false
```
{: .repl }

<aside class="tip">
  Ruby doesn’t force you to use <code>?</code> for Boolean-returning methods, but it’s a strong convention in the community. When you see a method ending in <code>?</code>, you can safely assume it will give you <code>true</code> or <code>false</code>.
</aside>

## 11. Syntax Sugar

*Syntax sugar* is a programming term for shortcuts in the language, ways of writing code that are more concise and pleasant without adding new capabilities. Ruby strings have several operators that act as shorthand for existing methods.

### `<<` (shovel operator)

Appends text to the end of a string. Equivalent to calling `String#concat`

### `[]` (square brackets)

Extracts a character or substring by index or range. Equivalent to calling `String#slice`.

### `==` (equals)

Checks if two strings are exactly the same. Equivalent to calling `String#eql?`.

```ruby
pp "test"[0..1]         # => "te"       (same as "test".slice(0..1))

greeting = "Hi"
greeting << "!"         
pp greeting             # => "Hi!"      (same as greeting.concat("!"))

pp "apple" == "apple"   # => true       (same as "apple".eql?("apple"))
```
{: .repl }

<aside class="tip">
  <strong>Tip:</strong> These operators are just "sweetened" syntax. They don't add new powers. Under the hood, Ruby calls the regular string methods. Once you understand the method form, the sugar makes your code shorter and friendlier to read.
</aside>

## Wrap-Up

You've learned:

- How to create, concatenate, and interpolate strings
- How to get input with `gets` and clean it with `chomp`
- Common methods (`strip`, `upcase`, `reverse`, etc.)
- String replacement with `gsub` and regex
- Encodings, ASCII codes, and `ord`/`chr`
- Mutability and immutability (freeze)
- Ruby's convention for `!` methods

## Quiz

- Why should you use `chomp` with `gets`?
- To remove the newline character at the end of input.
  - Correct! Otherwise, input will include `\n`.
- To convert input into an integer.
  - Not correct. `chomp` doesn't change types.
- To force uppercase letters.
  - Incorrect. That's `upcase`.
{: .choose_best #chomp title="Using Chomp" answer="1"}

- Which of these operations are valid on Ruby strings?
- <code>"hi" << " there"</code>
  - Correct! </code><<</code> appends text.
- <code>"hi".freeze << "!"</code>
  - Not correct. Frozen strings cannot be modified.
- <code>"A".ord</code>
  - Correct! Converts character to its ASCII/Unicode code.
- <code>123.chars</code>
  - Not correct. Only strings respond to </code>.chars</code>.
{: .choose_all #string_ops title="Valid String Operations" answer="[1,3]"}

## Project: String

In this project, you will write Ruby programs that leverage these string methods. This project includes automated tests, so click this link to get started <https://github.com/dpi-tta-projects/ruby-string/fork>, fork the repository and create a codespace.

<aside class="warning">
  In order to get credit for completing this project you'll need to open the assignment link from canvas to generate an access token.
</aside>

## References

- [Ruby Docs: String](https://ruby-doc.org/3.4.1/String.html)
