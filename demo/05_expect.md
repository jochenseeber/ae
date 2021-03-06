# Expect Method

Expect is another assertion nomenclature available for use in your
tests or specifications. Inspired by Jay Fields' Expectations library,
it provides convenient syntax for creating exception and case equality
assertions.

    require 'ae/expect'


## Underlying Comparison

Expect uses `#===` for comparison. So providing an argument and a block
to #expect we can test for a somewhat broader range of compassion
than #assert. For example we can test for a subclass.

    expect Numeric do
      3
    end

  Assertion.assert.raised? do
    expect Numeric do
      "3"
    end
  end


## Exception Expectation

If the comparator is an Exception class or a instance of an Exception class,
then #expect will check to see if the block raises that kind of exception.

    expect StandardError do
      some_undefined_method
    end

    expect Assertion do
      expect(nil)
    end

This is an important distinction to note because it means `#expect` can not be used
if verify instances of Exception classes.

    Assertion.assert.raised? do
      expect Exception do
        Exception.new
      end
    end


## Regex Expectations

That #expect entails `#===` also means we can check for Regexp matches.

    expect /x/ do
      "oooxooo"
    end


## Expected Method

We can use #expected to make the receiver the object of expectation.

    x = "dummy"

    /x/.expected do
      "x"
    end


## Without Block

Without a block, the receiver is compared to the argument.

    x.expect String


## Negative Forms

Like #assert, `#expect` has a negated form called #expect!

    expect! /x/ do
      "o"
    end

The pure word form for those who do not like the clever use of the
explimation mark is #forbid.

    forbid /x/ do
      "o"
    end


## Functor, or Higher Order Function

Like #assert, #expect can be used used as a *fluid* notation.

    10.expect == 10

In which case it works just like `#assert`, including negative forms.

    10.expect! == 11
    10.forbid  == 11

