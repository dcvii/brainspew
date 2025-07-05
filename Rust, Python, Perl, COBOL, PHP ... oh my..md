---
title: "Rust, Python, Perl, COBOL, PHP ... oh my."
source: "https://dataengineeringcentral.substack.com/p/rust-python-perl-cobol-php-oh-my"
author:
  - "[[Daniel Beach]]"
published: 2025-06-23
created: 2025-06-26
description: "a tale of some languages (Anonymous Rust Dev)"
tags:
  - "clippings"
---
### a tale of some languages (Anonymous Rust Dev)

![](https://substackcdn.com/image/fetch/$s_!4COo!)

We all love our little language wars: *the vitriol, the expletives, the dank memes that accompany them.*

You may recall, as your friendly neighborhood **Anonymous Rust Dev**, that I've been magnanimous and kind to the Python language. This is because I'm above it all - I can find the beauty in any language if I look hard enough, and I'm willing to give credit where it's due.

But even I have my breaking point, which I'd like to explore today. How clunky does a language need to be to make itself my foe?

## The baselines

Well, I can't sit here and talk up a language without the receipts. So I'll set some ground rules that I'll use as the basis for my "highly objective" analysis.

![](https://substackcdn.com/image/fetch/$s_!WTsz!)

1. It's okay to use third-party libraries, but more points go to a well-organized dependency-management ecosystem, and deducted for having to scrape snippets out of some decades-long-lost comment buried in an [experts-exchange.com](https://go.experts-exchange.com/) thread.
2. Code (including dependencies) should be readable and lend itself well to understanding the problem it's solving.
	1. *Comments are an insufficient crutch to carry a language's expressivity; the code itself needs to be self-explanatory to such a degree that a C-suite executive could look at it and understand at a high level what's going on (assuming good variable and function naming conventions are followed).*
3. While I don't kowtow to language popularity (else, I'd probably be a Java dev), points will be deducted if a language is obscure and nobody is left who knows how to maintain our code in the future.
4. Whatever is chosen should be backed by a standard, and we won't favor variants.
	1. *Meaning, if we chose something like SQL, we'd base our results off of the standard and not some flavor like MySQL.*
5. The difficulty of creating a new project and building it is assessed. One-liners are favored, while tedious hand-edited build scripts or arcane commands are penalized.
	1. *No points removed for reaching into the third-party ecosystem to find a useful build tool that manages this pain (e.g. using* `yarn` *instead of* `npm`*).*

> Point 3 automatically rules out some obvious choices, such as [Brainfsck](https://en.wikipedia.org/wiki/Brainfuck) or [ArnoldC](https://lhartikk.github.io/ArnoldC/). Also, despite what I say in #4, I don't think SQL qualifies for this discussion, as it's not technically a "programming" language (probably [no love lost here](https://www.confessionsofadataguy.com/sql-bad-reddit-mad/), anyway).

***Thanks to [Delta](http://www.delta.io/) for sponsoring this newsletter! I personally use Delta Lake on a daily basis, and I believe this technology represents the future of Data Engineering. Content like this would not be possible without their support. Check out [their website](http://www.delta.io/) below.***

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/708be49f-dfaa-498f-a862-8e9810a5fc58_600x123.webp%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:123,%22width%22:600,%22resizeWidth%22:null,%22bytes%22:4196,%22alt%22:%22%22,%22title%22:%22%22,%22type%22:%22image/webp%22,%22href%22:%22http://www.delta.io%22,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:null,%22isProcessing%22:false,%22align%22:null,%22offset%22:false%7D)

## Getting Started

Regarding the exercise in question, we aim to transform a simple CSV file into a semi-structured JSON file. Our data source will be located in **/tmp/test.csv** and have the following raw contents:

```markup
last_name,first_name,age
Jones,Steve,3
Smith,Nick,50
```

Yeah, it's hardly the fanciest thing out there, but we're not looking to make this a complicated test.

Output will be saved to **/tmp/test.json**. I don't particularly care if it's formatted for readability or compactness, though in the real world, you'd want a library capable of managing such details.

## First contender: Rust

Our journey here starts in the CLI:

```markup
$ cargo new csvtojson_rs && cd csvtojson_rs
$ cargo add serde serde_json csv --features serde/derive
```

My **src/main.rs** file:

```markup
use serde::{Deserialize, Serialize};

const PATH_TO_CSV_FILE: &str = "/tmp/test.csv";
const PATH_TO_JSON_FILE: &str = "/tmp/test.json";

#[derive(Debug, Deserialize, Serialize)]
struct Person {
    pub last_name: String,
    pub first_name: String,
    pub age: i32,
}

fn main() {
    let reader = csv::Reader::from_path(PATH_TO_CSV_FILE).expect("should open test csv file");
    let mut output = vec![];

    for row in reader.into_deserialize() {
        let person: Person = row.expect("should be valid person");

        output.push(person);
    }

    std::fs::write(
        PATH_TO_JSON_FILE,
        serde_json::to_string(&output).expect("should serialize to JSON"),
    ).expect("should write file to disk");
}
```

In this example, I did the work of defining the schema via the `Person` struct, and handled the possible errors using the less-than-graceful approach of `.expect()`. Whatever, this is a get-it-out-the-door effort.

```markup
$ cargo run
```

In this Rust-based example, I leaned very heavily into third-party crates for serialization and deserialization for the different formats. In particular, `serde` carries us, handling both the CSV and JSON side of the equation under the hood.

## Second contender: Python

Again, from the CLI side:

```markup
$ uv init csvtojson_py && cd csvtojson_py
```

...and our resulting **hello.py** file:

```markup
import csv
import json

PATH_TO_CSV_FILE = "/tmp/test.csv"
PATH_TO_JSON_FILE = "/tmp/test.json"

def main():
    recs = []
    with open(PATH_TO_CSV_FILE) as csv_file:
        csv_reader = csv.DictReader(csv_file)
        for row in csv_reader:
            recs.append(row)

    with open(PATH_TO_JSON_FILE, 'w') as json_file:
        json_file.write(json.dumps(recs))

if __name__ == "__main__":
    main()
```

Execution is simple, too:

```markup
$ uv run hello.py
```

> *You'll note that, unlike Rust, the JSON and CSV libraries are components of the Python Standard Library. This makes sense from both Rust and Python's perspective - in the case of Python, they're both so ubiquitous that making them a well-supported function of the language runtime costs little and offers much.*

In Rust's case, owing to its use as a systems language, many of its applications are built without the benefit of the standard libraries ("no-std"), which is frequently seen in embedded applications; in that case, serde (and its derivatives like the CSV and JSON libraries) are decoupled from the standard library and can be used in no-std environments.

## A blast from the past - Perl

Okay, I know people still use perl for some reason, which thankfully also has its own third-party ecosystem (CPAN) to get around having to regex our way through a delimited text document.

If you're familiar with CSV, you know that there are many variants and idiosyncrasies (optional text wrapping, multiline values, escape characters) to complicate things, and having to write a regex to handle this (which I believe is the perl way to do it) would not be pleasant.

> In case you're curious about what I feared having to write: [this SO answer](https://stackoverflow.com/a/3068793) gives a good representative example.

I've never used CPAN before, so had to hit up the [installation](https://www.cpan.org/modules/INSTALL.html) instructions to do this. At least here in Kubuntu, I have no problems just firing up `cpan` or `perl` at the CLI, but chose to go through their `cpanm` installation process, which forced me into a sudo prompt:

```markup
$ cpan   # Ran this guy first just to force me through its onboarding prompts; note the profile script recommendations
         # it gives at the end of the process.
$ sudo cpan App::cpanminus
```

With that done, let's try creating a new project:

```markup
$ mkdir csvtojson_pl && cd csvtojson_pl
$ sudo cpan Text::CSV   # Got yelled at when I tried it without sudo; very frustrating.
```

To bootstrap this process, since again I'm new at this, I wanted to first know whether I could read my file, and what I was looking at data-wise:

```markup
use Data::Dumper;
use Text::CSV qw(csv);

my $doc = csv(in => "/tmp/test.csv", headers => "auto");

print Dumper($doc);
```

Running my script gives me:

```markup
$ perl script.pl
# $VAR1 = [
#           {
#             'age' => '3',
#             'last_name' => 'Jones',
#             'first_name' => 'Steve'
#           },
#           {
#             'age' => '50',
#             'last_name' => 'Smith',
#             'first_name' => 'Nick'
#           }
#         ];
```

Okay, this is what I like to see. Now to figure out the JSON part.

First, I went to install the JSON library, but CPAN told me it was already installed?

```markup
$ sudo cpan JSON
```

Looking at the [docs](https://metacpan.org/pod/JSON), it seems straightforward to use, so I'll just give it the old community college try:

```markup
use Text::CSV qw(csv);
use JSON;

my $csv_path = "/tmp/test.csv";
my $json_path = "/tmp/test.json";

my $in_doc = csv(in => $csv_path, headers => "auto");
my $out_doc = encode_json $in_doc;

open(JSON_OUT, ">", $json_path) or die $!;
print JSON_OUT $out_doc;
close(JSON_OUT);
```

Working with the file API kind of reminds me of VB6. Otherwise, this was surprisingly less ugly and painful than I originally thought it would be.

Telling my code `do something... or die` does feel a bit fatalistic, and I never got to `chomp` on anything, but CPAN smoothed over a lot of pain points. While I'd probably never choose to author a new perl script in the future, I can at least rest assured that if the occasion does arise it's not as gnarly as I feared.

> *Actually, the bad rep that perl has with me seems undeserved, but [the internet](https://www.reddit.com/r/linuxadmin/comments/sy08jz/why_the_perl_hate/) acknowledges some good reasons for its general reputation.*

Also worth mentioning: perl (v5) is almost certainly available out-of-the-box on \*nix systems, so if you (like me) hate writing bash scripts, this might be a good alternative.

## COBOL

I'm doing this one on a dare. My compiler of choice is ~~OpenCOBOL~~ [GnuCOBOL](https://gnucobol.sourceforge.io/). I wrote some of this stuff back in my college days, and I don't remember it being all that bad.

Just to be clear, I think greenfield development in COBOL would be stupid. However, just as C++'s death in the face of Rust is very premature, so also is COBOL's demise, given just how much running (and working, I might add) code is out there in the wild today. You don't fix what ain't broke, and that means this language still might be worth picking up even in 2025.

Looking at GnuCOBOL's [docs](https://gnucobol.sourceforge.io/faq/index.html#using-gnucobol), we learn how to install it. Well, I went ahead and already tried it with `apt install gnucobol` and was met with success, but if you want to try building from source then this is a good starting point. I also suspect you'll find a docker container if you don't want to install this stuff on your computer.

### Thinking differently about files

Okay, so disclaimer: my trivial test CSV file turns out to be a happy accident. COBOL has a function called [UNSTRING](https://www.mainframestechhelp.com/tutorials/cobol/unstring-statement.htm) that does the heavy lifting for us, but would have struggled with some of those earlier-mentioned idiosyncrasies I brought up in the perl section. For our purposes today, I think we'll have no trouble, but I suspect that arcane file formats might not be COBOL's greatest strength.

Which takes us to JSON, which is surprisingly supported in COBOL via commands like `JSON GENERATE` or `JSON PARSE`. I guess I shouldn't be terribly surprised; as stated already, people still write COBOL, and the language has evolved to help modern developers keep writing code for the current age.

Well, now that the feasibility study is complete, let's give it a go.

```markup
$ mkdir csvtojson_cob && cd csvtojson_cob
```

...and our **program.cob** file:

```markup
IDENTIFICATION DIVISION.
       PROGRAM-ID. CsvToJson.
       AUTHOR. AnonymousRustDev.
       
       ENVIRONMENT DIVISION.
       INPUT-OUTPUT SECTION.
       FILE-CONTROL.
           SELECT CSVIN ASSIGN TO "/tmp/test.csv"
                  ORGANIZATION IS LINE SEQUENTIAL.
           SELECT JSONOUT ASSIGN TO "/tmp/test.json".
       
       DATA DIVISION.
       FILE SECTION.
       FD CSVIN
           BLOCK CONTAINS 0 RECORDS
           DATA RECORD IS TEXT-LINE.
       01 TEXT-LINE PIC X(1000).
       FD JSONOUT
           BLOCK CONTAINS 0 RECORDS
           DATA RECORD IS JSON-TEXT.
       01 JSON-TEXT PIC X(1000).

       WORKING-STORAGE SECTION.
       01 PERSON-RECORD.
           02 last_name PIC X(20).
           02 first_name PIC X(20).
           02 age PIC 9(2).
       01 JSON-CURRENT PIC X(255) VALUE SPACES.
       01 COUNTER PIC 9(1).
       
       PROCEDURE DIVISION.
       Begin.
           OPEN INPUT CSVIN.
           OPEN OUTPUT JSONOUT.

           STRING '[' INTO JSON-TEXT
           WRITE JSON-TEXT.

      *    Skip the first (header) row:
           READ CSVIN
           END-READ

           PERFORM UNTIL EXIT
                READ CSVIN INTO TEXT-LINE
                    AT END EXIT PERFORM
                END-READ

                UNSTRING TEXT-LINE DELIMITED BY ','
                    INTO last_name, first_name, age
                END-UNSTRING

                JSON GENERATE JSON-CURRENT FROM PERSON-RECORD
      *             Without the omit, the entity type name is the parent key
                    NAME OF PERSON-RECORD IS OMITTED
                    ON EXCEPTION
                        DISPLAY 'No can do.'
                    NOT ON EXCEPTION
                        DISPLAY 'generated'
                END-JSON

                IF COUNTER > 0 THEN
                    STRING ',' DELIMITED BY SIZE,
                        function trim(JSON-CURRENT) DELIMITED BY SIZE 
                        INTO JSON-TEXT
                    END-STRING
                ELSE
                    STRING function trim(JSON-CURRENT) DELIMITED BY SIZE 
                        INTO JSON-TEXT
                    END-STRING
                END-IF
                WRITE JSON-TEXT

                ADD 1 TO COUNTER
           END-PERFORM

           INITIALIZE JSON-TEXT
           STRING ']' INTO JSON-TEXT
           WRITE JSON-TEXT.

           CLOSE CSVIN.
           CLOSE JSONOUT.
```

...I hate it.

That was the worst programming experience I think I've had in years. I couldn't figure out how to create a variable-length array, so ended up having to mash JSON records together by hand.

> *And finding a version of GnuCOBOL that actually supports the JSON GENERATE command correctly took effort; much time was lost just troubleshooting why my strings failed to actually exist until I stumbled upon a [v4.0 Docker container](https://github.com/brazilofmux/gnucobol/tree/ec57c7165e94ec0e13fa1dc1c31f9f1e2123b9d6/4.0).*

Try to google for anything COBOL-related, and IBM hits are at the top of the list, except everything they give you to work with is a [cryptic BNF diagram](https://www.ibm.com/docs/en/cobol-zos/6.3.0?topic=statements-unstring-statement) with little by way of example usage (yes, I'm that stupid, I need examples to figure stuff out). Like, I grew up in the early 90s era with a DOS 4.0 manual explaining how to use the `debug` command to hand-roll assembly, and that was a cakewalk by comparison.

Somebody please brain me with a rusty spork if I ever suggest writing COBOL again. And I'm sure some avid COBOL dev looks at what I wrote, shakes their head in disdain, and my feelings are only even more validated in the process; no part of this process was intuitive or easy, and my code is obviously ham-fisted.

## PHP

I needed a palate cleanser after that last one, so I reached for a breath of fresh air: PHP, the beloved and ubiquitous language everybody reaches for when... uh, Wordpress, I suppose.

First, if you're on Linux or Mac, chances are you either have PHP or can get it very quickly through a package manager. Windows has installers too, so low-hanging fruit.

```markup
<?php
$csv_in = trim(file_get_contents('/tmp/test.csv'));

// So it goes without saying that there are libraries or other techniques for this,
// but I'mma hand-roll this beast:
$lines = explode("\n", $csv_in);
$first_line = array_shift($lines);
$object_keys = explode(',', $first_line);

$records = [];

foreach($lines as $current_line) {
    $as_split = explode(',', $current_line);
    $records[] = array_combine($object_keys, $as_split);
}

file_put_contents('/tmp/test.json', json_encode($records));
```

For those already in the know, it must be painful seeing me not reach for Composer. There is a perfectly useful [CSV library](https://github.com/thephpleague/csv) that I've had great success with, and others may already be aware that some of the `explode` stuff would go away if I used the shorthand helper `str_getcsv`. Nonetheless, it only gets simpler than what I did above (at least for our trivial CSV file).

## Weighing in our contestants

Now that you've seen the code and the struggles involved, here's how I'd rate things in terms of my earlier bullet points:

### Third-party ecosystem

For this one, the only one that doesn't get any points is COBOL - not because no ecosystem exists, but I've spent far too much time trying to get any meaningful information out of that community. For everybody else, full points awarded for having a rich and diverse ecosystem from which to pull any needed already-solved solutions.

### Code as prose

It's hard to be fair here - it's such a subjective thing, after all.

First, I wanted to award full points to COBOL, as this was its original claim to fame after all. But, looking at what I wrote earlier, I don't think this is necessarily true - there might be a lot of English in there, but it isn't exactly readable outside of the `PROCEDURE DIVISION` portion.

The `FD` declarations feel like they're trying too hard to be human-readable, but contrast with the `PIC` declarations (I think it means "picture"? Like my data is some kind of drawing?).

Meanwhile, I came into this thinking perl would be cryptic and arcane, but it ended up feeling a lot more like PHP or Python in my own opinion.

And, let's not lie to ourselves, the Rust language has a reputation for being complex. My example doesn't really demonstrate just how quickly the code can get gnarly to a novice reader, but if you're just encountering it for the first time today in this article, I'd assume you'd rate it lower than the "P-languages" (perl, Python, PHP). In the interest of fairness, I'll make that judgment call for you here and now - the "P-languages" win, followed by Rust, and finally COBOL.

### Obscurity

COBOL and perl are the obvious examples here of "yesterday's news" in terms of languages, with the former being a glaring example of something that people want to distance themselves from. Yes, people still learn COBOL in this day and age, but it's a rarity and not representative.

Likewise, despite its availability, perl has a lot going against it. Aside from a few old GNU types, there probably aren't a lot of advocates for the language floating around, and my casual searching for info while composing this article tells me that even seasoned perl devs find it to be flawed.

Many probably wish PHP would go the same route, but it unfortunately continues to improve over time and is actually a halfway decent language. I'd actually put it a bit higher than Python, particularly where OOP and types are concerned, as in my own experience the Python type hints are more of a gentle suggestion than something that's actually enforced.

Rust is soon to have its day, evidenced in incremental grabs of market share year-over-year. It's not yet found a mainstream place - a lot of developers wish there were more Rust jobs than there actually are, and businesses are still hesitant to adopt it for assorted reasons (e.g. the relatively smaller talent pool than a "boring" language like Java).

And then there's Python, which is easily the most popular of the pack. I won't even spend any time discussing it, it's pretty self-evident.

### Standards

GnuCOBOL feels like it's trying to be the MySQL of the COBOL community. I assume that all the enterprise-level COBOL devs are running IBM or some other mainframe flavor, and my impression is that GnuCOBOL is the spunky new kid that's racing to catch up to the old guard. The trouble I had with `JSON GENERATE` really drives this home - while I did eventually succeed with that v4.0, the one that came out of my Ubuntu repository left me with [this mess](https://eklausmeier.goip.de/blog/2021/08-17-generating-json-with-cobol).

### Launching a new project

Thanks to `uv`, I won't take any points away from Python; normally, my experience with `venv` and `pip` leave much to be desired, but today's exercise shows how easy it can be.

Had I bothered with `composer`, the PHP example would have been fairly straightforward.

Even with perl, the CPAN repository is perhaps the grandpappy of library management as we know it today.

Rust's `cargo` is perhaps my own favorite, on par with `uv` with regards to its ease-of-use.

That leaves COBOL. I'm really not sure how to categorize this; all I did was create a.cob file and call it a day, but I have no idea how this scales when you start adding dependencies. I hope to never find out.

## Is there a takeaway here?

For me, this was a chance to play with some stuff I normally don't get to touch. I'm not about to abandon my current ways of doing things after this exercise, but hopefully for those on the fence you can see that it's not really all that scary out there in terms of other languages.

Granted, I didn't touch some of the weirder stuff, and probably skipped over your favorite language in the process (any Ada fans out there? Fortran? Lua?). Feel free to write your own article espousing how I glossed over the greatest language known to man, and I will gladly read it.