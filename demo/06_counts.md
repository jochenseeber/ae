# Assertion Counts

AE tracks the number of assertions made and the number that failed to pass.
We can reset the count using the +recount+ class method.

    old_counts = AE::Assertor.recount

For example if we have one assertion pass and another fail.

    assert(true)

    expect Assertion do
      assert(false)
    end

We will see that AE counted three assertions and one failure.

    counts = AE::Assertor.counts.dup

    counts[:total].assert == 3
    counts[:pass].assert  == 2
    counts[:fail].assert  == 1

The #expect call is an assertion too, which is why the total count is 3
rather than 2.

Now that we are done checking counts we will restore them so that
any other demos being run with this will tally correctly.

    AE::Assertor.recount(old_counts)
    AE::Assertor.counts[:total] += 3
    AE::Assertor.counts[:pass]  += 3

