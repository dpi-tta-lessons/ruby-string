

<!-- computers think in 1s and 0s, humans think more using written word -->

<!-- TODO: history of chars (under the hood), string, ascii, hex, octal, unicod (utf-8) 

"test".encoding
-->

<!-- TODO: slices [] -->
<!-- TODO: casing -->
<!-- TODO: chomp -->
<!-- TODO: gets -->
<!-- TODO: concatenation (concat, +) << -->
<!-- TODO: interpolation -->
<!-- TODO: substitution methods (gsub / regex) -->
<!-- TODO: multiplication / addition -->
<!-- TODO: strip -->
<!-- TODO: chars -->
<!-- TODO: length -->
<!-- TODO: reverse -->

<!-- TODO: comparison .eql? == -->

<!-- TODO: mutable / immutable (freeze) -->

<!-- syntax sugar ==, [], << etc. -->

<!-- TODO: https://ruby-doc.org/3.4.1/String.html -->

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

<aside class="tip">
  Strings are text, not numbers. The string <code>"1"</code> is different from the number <code>1</code>.
</aside>

## 1. Creating Strings

You can create strings with double quotes (`"`) or single quotes (`'`).

```ruby
greeting = "Hello, world!"
farewell = 'Goodbye!'
```
{: .repl }

<!-- TODO: String.new ??? -->

## 2. Concatenation and Interpolation

<!-- TODO: use .concat method first, syntax sugar later -->
A key characteristic of strings is that they are treated as text, not numerical values; for instance, the string `"1"` is different from the number `1`, and adding two strings like `"1" + "2"` results in the concatenated string `"12"` rather than the number `3`.

Strings can be combined with `concat`, `+`, or `<<`. This is called *concatenation*.

```ruby
first = "Hello"
second = "World"

puts first.concat(" ", second)
puts first + " " + second
puts first << " " << second
```
{: .repl }

*Interpolation* lets you insert variables directly inside double-quoted (`""`) strings. Notice in this example how we use the hash and curly braces inject the name variable into the string.

```ruby
name = "Ruby"
puts "Hello, #{name}!"
```
{: .repl }

<aside class="warning">
  <strong>Note:</strong> Interpolation works only with double quotes <code>"</code>, not single quotes <code>'</code>.
</aside>

## 3. User Input

Ruby's `gets` method reads user input.

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

## 4. Common String Methods

```ruby
word = " hello "

puts word.strip       # "hello"
puts word.upcase      # " HELLO "
puts word.downcase    # " hello "
puts word.capitalize  # " hello " → " hello "
puts word.reverse     # " olleh "
puts word.length      # 7
```
{: .repl }

## 5. Indexing and Slices

Strings work like lists of characters. 

![array of charaters](https://upload.wikimedia.org/wikipedia/commons/6/6b/String_example.png)

You can access single characters or slices using square brackets.
<!-- TODO: how to do this without [] syntax sugar -->
<!-- TOOD: note on ranges (1..2) -->
```ruby
text = "Ruby"

puts text[0]     # "R"
puts text[1..2]  # "ub"
puts text[-1]    # "y"
```
{: .repl }

## 6. Substitution with `gsub` and regular expressions

`.gsub` replaces text. With regular expressions (regex for short), it becomes even more powerful.

<!-- TODO: more common regex examples -->

<!-- 

s = 'hello'
s.sub(/[aeiou]/, '*') # => "h*llo"
s.gsub(/[aeiou]/, '*') # => "h*ll*"
s.gsub(/[aeiou]/, '')  # => "hll"
s.sub(/ell/, 'al')     # => "halo"
s.gsub(/xyzzy/, '*')   # => "hello"
'THX1138'.gsub(/\d+/, '00') # => "THX00"

-->

```ruby
phrase = "I have 3 cats and 2 dogs."

puts phrase.gsub(/\d/, "#")        # Replace digits
puts phrase.gsub(/cats?/, "birds") # Replace "cat" or "cats"
```
{: .repl }

## 7. Character Codes and Encoding

<!-- TODO: add details on ascii, utf-8, etc. -->
Strings are sequences of bytes with an encoding (UTF-8 by default).

```ruby
puts "Ruby".encoding    # UTF-8
puts "A".ord            # 65 (ASCII code for 'A')
puts 65.chr             # "A"
```
{: .repl }

## 8. Mutability and `freeze`

Strings in Ruby are *mutable* (you can change them).

```ruby
s = "Hi"
s << " there"
puts s   # "Hi there"
```
{: .repl }

You can make a string *immutable* (you can't change it) using the `freeze` method.

```ruby
name = "Bob".freeze
name << "by"   # Raises FrozenError
```
{: .repl }

<!-- ## Beware the Bang (!) Operator

<aside class="tip">
  In Ruby, methods with <code>!</code> usually modify the string in place.
  For example: - `"hello".upcase` returns a new string `"HELLO"` - `"hello".upcase!` permanently changes the string to `"HELLO"`
</aside> 

-->

## 9. Syntax Sugar

Ruby gives shortcuts for common string operations:

<!-- shovel -->
<< → append

<!-- square brackets -->
[] → slice

<!-- equals -->
== → compare

<!-- multiply -->
* → repeat

```ruby
puts "ha" * 3      # "hahaha"
puts "test"[0..1]  # "te"
```
{: .repl }

## 10. String Comparison

```ruby
puts "apple" == "apple"   # true
puts "apple".eql?("Apple") # false
puts "a" < "b"            # true (alphabetical)
```
{: .repl }

Practice Challenge

## Wrap-Up

You've learned:

- How to create, concatenate, and interpolate strings
- How to get input with `gets` and clean it with `chomp`
- Common methods (`strip`, `upcase`, `reverse`, etc.)
- String replacement with `gsub` and regex
- Encodings, ASCII codes, and `.ord`/`.chr`
- Mutability and immutability (freeze)
- Ruby's convention for `!` methods

## Quiz

- Why should you use `.chomp` with `gets`?
- To remove the newline character at the end of input.
  - Correct! Otherwise, input will include `\n`.
- To convert input into an integer.
  - Not correct. `.chomp` doesn't change types.
- To force uppercase letters.
  - Incorrect. That's `.upcase`.
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
