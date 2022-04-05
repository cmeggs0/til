---
layout: post
title: "Some of the stuff that I learned during Ruby Koans"
---
### Arrays
- Buildarray = [1,2]
- Range.to_a
- .push(:last) – adds element to end of array
- .pop – removes last element of an array
- .shift – same as pop, but first element
- The unshift() method adds one or more elements to the beginning of an array and returns the new length of the array.
- Splat operators
### Objects
- Everything is an object
- Inspect() returns a string
- Integers object id = n*2+1, works for negatives as well
- .clone creates a different object
### Hashes
- {} empty hash
- Can use objects attached to strings in hashes for easy recall, hash key
- Hash order doesn’t matter, as long as hash keys match
- .merge to add to hash
- Unsure about:

  def test_default_value_is_the_same_object
    hash = Hash.new([])
 
    hash[:one] << "uno"
    hash[:two] << "dos"
 
    assert_equal ["uno", "dos"], hash[:one]
    assert_equal ["uno", "dos"], hash[:two]
    assert_equal ["uno", "dos"], hash[:three]
 
    assert_equal true, hash[:one].object_id == hash[:two].object_id
    
- I think if you create a default hash, doesn’t register keys
 
### Methods
 
- Can create our own methods in ruby
- Can add default values
- def method_with_defaults(a, b=:default_value)
    [a, b]
  end
- With explicit return, return “return” value
- Without explicit return, returns last value
- Keyword Arguments
- Always have a default value, making them optional to the caller

### Constants
- Nested constants over inherited constants, except with explicit scoping
 
### Regular Expressions
 
- //.class = Regexp (Regular Expression)
- "string”[/search string/]
- ? – optional
- + - one or more
- * - zero or more
- animals.select { |a| a[/[cbr]at/] }
- provides multiple options cat, bat, rat.
- .select makes sure it iterates through whole array
- [/[0123456789]+/] = [/\d+/] = [/[0-9]+/]
- [/\s+/] – search for string beginning with whitespace


  def test_a_character_class_can_be_negated
    assert_equal "the number is ", "the number is 42"[/[^0-9]+/]
  end
  
  
- [/\d+/] – search for digit character class
- [/\w+/] – search for a word character class
- Can capitalize any of these to negate or add ^ in front 
- \A to anchor to the front of a string
- \z (at the end) to anchor to the end of a string
- ^\d – search for digit at the start of lines
- \d$ - search for digit at the end of lines
- \b anchors to word boundary
- () groups content, can also be used to content match by number, or access captures
- .scan finds all instances
- .sub – find and replace


  def test_sub_is_like_find_and_replace
    assert_equal "one t-three", "one two-three".sub(/(t\w*)/) { $1[0, 1] }
  end
 
  def test_gsub_is_like_find_and_replace_all
    assert_equal "one t-t", "one two-three".gsub(/(t\w*)/) { $1[0, 1] }
  end
 
### Control Statements
 
- If else sstatements
(true ? true value : falsevalue)
- Unless, is like if not true
- While statements
- Can use break unless or break if
- Next if
 
### Exceptions

  def test_exceptions_inherit_from_Exception
    assert_equal RuntimeError, MySpecialError.ancestors[1]
    assert_equal StandardError, MySpecialError.ancestors[2]
    assert_equal Exception, MySpecialError.ancestors[3]
    assert_equal Object, MySpecialError.ancestors[4]
  end
 
### Iterations
 
array.each { |item| sum += item } == array.each do |item|
      								sum += item
- .collect or .map transforms each element of an array
- .select or .fina_all selects certain elements of an array
- Files act as a collection of lines
