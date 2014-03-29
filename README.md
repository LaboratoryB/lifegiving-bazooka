Ethereum PoC3 Compatible Pyramid Scheme
---

**Life-Giving Bazooka? WTH?!**

Don't you want to buy this sweeeeet new device? It's the "Life Giving Bazooka" -- anything that it shoots is magically healed! It's the best thing to happen to the world! Wouldn't you want to invest in this?

Of course you don't! Because a life giving bazooka, doesn't exist. It's just not possible.

Just like any sort of [macguffin](http://en.wikipedia.org/wiki/MacGuffin), it's just something to tempt you. Here's a silly Pyramid scheme, "Make $N at home per week! $N is clearly too much! *BUY THIS BOOK*". But what does that book do for you? Well it doesn't do anything but say that you gotta pay in, in order to sell more copies of that book. The book, is just a macguffin. And it's just a never ending cycle of sell this book.

In this example, that's our macguffin for the pyramid scheme -- the life giving bazooka.

*According to the U.S. Federal Trade Commission, many [multi-level marketing] schemes "simply use the product to hide their pyramid structure."* -Wikipedia

---

**Isn't that... dirty?**

It demonstrates a little pyramid scheme scheme. It's intended to be categorically, "a bad deal". 

Sounds dirty? ...It's really one of things that makes Ethereum powerful, you can see the logic of a bad deal quite visibly.

---

**How's it work?**

It's based on your classic [pyramid scheme](http://en.wikipedia.org/wiki/Pyramid_scheme). 

The person to originate the scheme is in the best position, as usual. So, the originator starts the chain, and then people who join -- reference his Ethereum address. 

So Let's stay Alice starts the chain. She invites Bob, and Charlie. Charlie invites Dave and Edward. We'll have a pyramid which looks like:

          Alice
          /   \
         /     \
        /       \
       Bob   Charlie
               /  \
              /    \
             /      \
            /        \
          Dave     Edward

When Charlie joins, let's say for 1 Ether. Alice gets, 100% of 1 Ether. When Edward joins, let's say for 2 Ether. Charlie gets 1 Ether, and Alice gets 1 Ether. 

When anyone joins, all their money goes up the chain, divided "evenly" between all of the references parents. It's still unfair, because we calculate a remainder for even division, and give the remainder to Alice.

Yep, it's that unfair.

---

**So let's actually use it**

Ok, first thing you'll do is compile this -- may I recommend my CLL preprocessor? https://github.com/dougbtv/cll-preprocess -- it contains a way to parse all of the comments and blank spaces from this file. It's got some submodules to make life easy. Once you do that, just copy and paste the EVM3-ASM code into your PoC3 client.

Let's review the three modes it has:

- Mode 0: Become the head of the pyramid
- Mode 1: Join the pyramid
- Mode 2: Withdraw Ether from contract

Mode 0 can only be run once. Mode 1 can be run, and Mode 2 requires that you have a balance in order to withdraw -- unless you're the head of the pyramid. Told ya, it's unfair!

So, let's create the contract, and let's say it winds up with address. `b690c13683cc5bc05ea5c5f51e4be0ddf64856e7`. We'll also pretend that your address is `100C4460453CCDEBF7C382C0A10AC6AD32544B08`

**Mode 0: Become the head of the pyramid**

You'll send to this contract (and it's expensive to run), so send it say `200 finney`. Send it one piece of data:

     0x00

The first data element is the mode. 0, 1, or 2. We use 0 for mode 0 (as you'd imagine). You can only run this once, and now... You're a real multi-level marketing marketeer (is that even a word?)

Now, you're set up. Let's have someone join.

**Mode 1: Join a scheme!**

Ok, now with mode one. We send two pieces of data, first: The mode. Second: The person who referred us. So, run this as an address different from your own -- best yet, your foes. Have them send mode 1, with your address the second piece of data. Have them send as much Ether as you can, 200 VEther at a minimum! (Just kidding, you can send it 200 finney again, or whatever).

So here's what that data will look like:

    0x01 0x100C4460453CCDEBF7C382C0A10AC6AD32544B08

You've got another member! Have them recruit and have more addresses join the scheme.

**Mode 2: Get that skrilla**

So your "bank role's on swole" (at least according to Snoop Dogg in *"Who Am I?"*). And you want to withdraw. It's easy, just send 2 as the mode, and the amount you want to withdraw as the second element, enter into the data window:

    0x02 250finney

---

*TO DO*

- Calculate fees. It doesn't do anything with the fees right now. Making balances relatively inaccurate.

---

*What's it look like under the hood?*

    @0x3E8     0x62C467A4A0E7F7DA54C538EA243866B52577F517 MUL 0
    @0x44C     0x62C467A4A0E7F7DA54C538EA243866B52577F517 ADD 0x905438E60010000 0x62C467A4A0E7F7DA54C538EA243866B52577F517 MUL 0
    @0x100C4460453CCDEBF7C382C0A10AC6AD32544B08     MUL STOP
    @0x62C467A4A0E7F7DA54C538EA243866B52577F517     ADD

Here's some data from the contract after it's been run.

I'll get into the details of this another time.

