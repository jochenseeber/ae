# Matchers

Matchers are simply Procs or objects with the proper interface that can be
passed to #assert or #refute (or other Assertor) as an ecapsulated test.

## Proc or #to_proc

Passing a Proc object or an object that responds to `:to_proc`, will use it
as if it were a block of the method. This allows for a simple way to quickly
create reusable assertions.

    palindrome = lambda{ |word| word == word.reverse }

    "abracarba".assert palindrome

## #matches?

Additionally if an object responds to #matches? then the receiver
will be passed to this method to determine if the assertion passes.

    palindrome = Object.new

    def palindrome.matches?(word)
      word == word.reverse
    end

    "abracarba".assert palindrome

## RSpec, Shoulda and other 3rd-Party Matchers 

With tha addition of #matches?, AE supports the same interface for matchers
as RSpec. Any matcher library designed for use with RSpec should therefore
be usable with AE as well. This includes RSpecs own matchers and Shoulda's
excellent Rails matchers.
