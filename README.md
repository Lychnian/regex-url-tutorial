![Regex URL](https://github.com/Lychnian/regex-url-tutorial/assets/140586279/b7866bdc-00ac-4608-83c0-580ce2915ca3)



# Regex URL Tutorial

Regular expressions, also known as regex, are a sequence or string of characters used to create search patterns. They are very useful in programming and web development, helping with tasks such as searching, matching, and editing text. Regex patterns can be simple or very detailed, using a range of special characters (metacharacters) and rules. This tutorial will provide a detailed examination of a specific regex pattern used for validating website addresses (URLs) in various web and data-related applications. 


## Summary

In this tutorial, we will examine a regex pattern that is designed to match different parts of a URL (Uniform Resource Locators) the addresses used to access resources on the internet. The Regex pattern we will examen in our tutorial for matching a URL is as follows:

## `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

This regex pattern effectively validates the standard URL (as in our tutorial sample URL) `https://www.examplesample.com/about-us` by sequentially matching its protocol or scheme `https://`, sub domain `www.` domain name `examplesample`, top-level domain `.com`, and path `/about-us`. 


![URL Anatomy](https://github.com/Lychnian/regex-url-tutorial/assets/140586279/4fe4e963-504f-4d40-8289-a7dd5f49e738)


The regex pattern ensures that each of these components is present and correctly formatted, making it a useful tool for URL validation in web development contexts. Let's dive in and explore how it functions!


## Table of Contents

- [Metacharacters](#metacharacters)
- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Author](#author)


## Regex Components

### Metacharacters
In regular expressions (regex), a metacharacter is a character that has a special meaning rather than representing itself. Each metacharacter serves a specific function in a regex pattern, allowing for the construction of complex and flexible search criteria expressions. When a metacharacter is used, it performs its special operation rather than matching its literal character in the text. For example, the regex `^a` would match any string that starts with `'a'`, not the literal string `'^a'`.  Metacharacters can signify various operations like the start or end of a line, quantification, grouping, and more.

Common metacharacters include:
*  `^` Caret - Represents the start of a line.
*  `$` Dollar Sign - Signifies the end of a line.
*  `.` Period - Matches any single character, except for line breaks.
*  `*` Asterisk - Matches zero or more occurrences of the preceding element.
*  `+` Plus Sign - Matches one or more occurrences of the preceding element.
*  `?` Question Mark - Makes the preceding element optional (indicating zero or one occurrence).
*  `|` Pipe - Acts as a logical OR.
*  `\` Backslash - Used as an escape character, to use metacharacters as literal characters.
*  `()` Parentheses - Used for grouping.
*  `[]` Square Brackets - Define a character class, matching any one character inside the brackets.
*  `{}` Curly Braces - Specify a specific amount of repetition.

Now that we have a foundational understanding of metacharacters and their role in shaping regular expressions, let's delve into how they are specifically utilized in our regex pattern. We'll explore metacharacters, including anchors, quantifiers, the OR operator, character classes, and more, to see how they function in the context of our URL-matching regex.


### Anchors `^`  and  `$` 

In our regex pattern `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`, the concept of anchors is represented by two symbols: the caret `^` at the beginning and the dollar sign `$` at the end. The caret `^` specifies that the match must start at the beginning of the string, indicating the position rather than matching a character. It ensures that the pattern matches only if it appears right at the start of the string.

Conversely, the dollar sign `$` at the end of the pattern asserts that the string must end at that point. This means that the regex will only match if the entire string conforms to the pattern right up to the end, without any extra characters following it.

In the context of our standard URL `https://www.examplesample.com/about-us`, the `^` anchor ensures that the regex pattern does not match a URL appearing in the middle of a text, but only if it's at the beginning. Similarly, the `$` anchor ensures that the pattern matches the URL up to its end, without any additional text. For example, the regex would not match a string where the URL is followed by extra unrelated characters. This combination of `^` and `$` is particularly important for accurately validating complete URLs, ensuring that the string being evaluated both starts and ends with the expected URL format, thereby framing the entire match within these boundary limits.

### Quantifiers `?`   `+`   `{2,6}`   `*`

In our regex pattern `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`, quantifiers play a vital role in determining how many instances of a particular character set or group are allowed. Let's examine the quantifiers present and see how they apply to our standard URL example `https://www.examplesample.com/about-us`.

Optional Protocol `?` in `(https?:\/\/)?`  `(https?` and `/\/?`

The optional protocol question mark `?` quantifier makes the preceding character or group optional, meaning that the character or group can either appear once or not at all in the string being matched. In our regex pattern `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`, the question mark `?` quantifier is used effectively in the following key places:

1. Optional 's' in Protocol `https?`:

Inside the protocol group, `?` directly follows ‘s’ in `https?`. This makes the 's' character optional, allowing the pattern to match both `http://` and `https://`. This usage of `?` effectively creates an OR condition between `http` OR `https`.
In our example URL, it matches the `https://` portion, but it would also match if it were just `http://`.

2. Optional Protocol `(https?:\/\/)?`:

Here, `?` follows the entire protocol group `(https?:\/\/)`, making this group optional. It means that the regex can match URLs whether they include the protocol `(http:// or https://)` or not. This functionality is akin to an OR operation - it matches URLs with OR without the specified protocol. In the context of our example URL `https://www.examplesample.com/about-us`, the `https://` part is present and gets matched by this group. If the URL started just with `www.examplesample.com/about-us` (omitting the `https://`), it would still match due to the `?` making the protocol optional.

3. Optional Trailing Slash `\/?$`: 

The `?` in `\/?$` near the end of the regex makes the trailing slash optional. This means the regex will match URLs that either end with a slash (/) or do not end with a slash. In the example URL, there is no trailing slash after 'about-us', and this is perfectly acceptable for the regex pattern, thanks to the `?` quantifier. It would match `https://www.examplesample.com/about-us/` (with a slash) as well as `https://www.examplesample.com/about-us` (without a slash).

The use of `?` in these contexts demonstrates its versatility, providing the flexibility necessary to match a variety of URL formats, accommodating the presence or absence of certain components such as the protocol and trailing slash.

Sub Domain and Domain Name `+` in `([\da-z\.-]+)`

The `+` quantifier following the character class `[\da-z\.-]` indicates that the preceding characters (digits, lowercase letters, periods, and hyphens) must occur at least once but can be repeated multiple times. This part of the regex matches the `www.examplesample` segment in our URL, ensuring that the sub domain and domain name consists of one or more of these allowed characters.

Top-Level Domain `{2,6}` in `([a-z\.]{2,6})`

The `{2,6}` quantifier specifies that the lowercase letters and periods in the top-level domain must occur at least 2 times but no more than 6 times. This matches the `.com` part of our example URL, fitting within the typical length range for top-level domains.

Path `*` in `([\/\w \.-]*)`

The `*` quantifier allows the characters in its preceding character class (slashes, word characters, spaces, periods, and hyphens) to appear zero or more times. This matches the `/about-us` portion of our URL, accommodating the possibility of having a path or having none, as this quantifier makes the path component optional.

In summary, the quantifiers in our regex pattern are essential for providing the flexibility and specificity needed to match various components of the standard URL. They ensure that each part of the URL, from the protocol to the path, is accurately identified and validated against the expected format.


### OR Operator  `|`

In regex, the pipe symbol `|` is the primary OR operator, used to specify alternatives within a pattern. This allows you to match one of several possible sequences. For example, red|blue matches either "red or "blue".

In our given regex pattern `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/,`, the OR operator as the typical pipe symbol `|` is not explicitly used, rather, the OR concept is represented subtly. It is integrated within specific segments permitting the pattern to recognize and match various potential forms of a URL by using features like optional characters `?` which we examined above, and character classes `[]`, which we will examen next. 

### Character Classes `[ ]`

A character class, denoted by square brackets `[]`, matches any one character from a set of characters defined within the brackets. In our regex pattern `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`, there are three sets of square brackets, each representing a character class that searches for specific patterns in parts of the URL. Here's a breakdown:

`[\da-z\.-]` (for characters in Domain Name, includes Sub Domain):
This character class matches any single digit `(\d)`, any lowercase letter from `'a'` to `'z'`, a period `(\.)`, or a hyphen `(-)`.
It is used to match the domain name portion of a URL. For example, in `https://www.examplesample.com/about-us`, it matches `www.examplesample`.

`[a-z\.]` (for characters in Top-Level Domain):
This character class matches any single lowercase letter from `'a'` to `'z'` or a period `(\.)`.
It is specifically used to match the top-level domain (TLD) of a URL, such as `.com` in `https://www.examplesample.com/about-us`.

`[\/\w \.-]` (for characters in Path):
This character class matches a forward slash `(\/)`, any word character (which includes letters, digits, and underscores as denoted by `\w)`, space, period `(.)`, or hyphen `(-)`. It is designed to match the path component of a URL, like `/about-us` in `https://www.examplesample.com/about-us`.

Each character class is tailored to match a specific format found in standard URL structures, ensuring that the regex pattern accurately validates the different parts of a URL.


### Grouping and Capturing `( )`

Building upon our understanding of character classes, denoted by square brackets [ ], which define a set of characters to be matched, we now transition to exploring "grouping and capturing" in regular expressions, signified by parentheses ( ). While character classes match any one character from a specified set, grouping and capturing allow us to treat multiple characters as a single unit and extract or manipulate these grouped characters. In our URL regex pattern, ( ) is used to define these groups, enabling us to isolate and work with specific segments of the URL, such as the protocol or domain. This distinction between [ ] for character classes and ( ) for grouping is fundamental in regex, providing us with a toolkit for intricate pattern matching and data extraction in strings like URLs.

In our regex pattern `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`, the concept of grouping and capturing is utilized to define specific parts of the URL. Grouping is done using parentheses `()`, which not only group elements of the regex together but also capture the content they match for potential use or reference. Let's look at how this is applied in our pattern and how it matches the sample URL `https://www.examplesample.com/about-us`.

Protocol Group `(https?:\/\/)?`

This group matches the protocol of the URL, either `'http'` or `'https'`. The `?` after https makes the `'s'` optional, thus allowing for both `'http'` and `'https'`. The entire group is followed by a `?`, making the presence of the protocol optional in the URL.
In `https://www.examplesample.com`, this group captures `https://`. If the URL started with just `'http://'`, it would match that as well.

Domain Name Group `([\da-z\.-]+)`

This group matches the domain name portion of the URL, including any combination of digits, lowercase letters, periods, and hyphens.
It captures `www.examplesample` in the URL `https://www.examplesample.com`.

Top-Level Domain Group `([a-z\.]{2,6})`

This group is designed to match the top-level domain (like .com, .org, .net), specifically capturing a sequence of lowercase letters and periods that are 2 to 6 characters in length. In the example URL, this group captures `.com`.

Path Group `([\/\w \.-]*)`

This final group matches the path of the URL, which can include a combination of slashes, word characters, spaces, periods, and hyphens. The `*` allows this part to be repeated multiple times or not appear at all. For `https://www.examplesample.com/about-us`, it captures the `/about-us` part.

Each of these groups not only helps in segmenting the regex for different components of the URL but also captures the corresponding parts of the URL. Capturing is particularly useful in scenarios where you need to extract or manipulate specific parts of the matched text, such as the domain name or path in a URL. In our regex pattern, these groups work collectively to validate and capture the essential parts of a standard web URL.


### Bracket Expressions `[ ]`

In our regex pattern `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`, you'll come across several bracket expressions, which are denoted by square brackets `[ ]`. These are just like the character classes we examined earlier. They let us match one character from a specific set that we choose.  For example, in our pattern, `[a-z]` means the regex can match any one letter from `'a'` to `'z'`.  

We use these bracket expressions in different parts of our URL pattern, like in the domain name and the path. They help us specify which characters are allowed in these parts of the URL. If you want more details on how these characters work in our regex pattern, refer back to the "Character Classes" section.


### Greedy and Lazy Match

In our regex pattern `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`, the concepts of Greedy and Lazy Matching come into play. These terms refer to how the regex engine handles quantifiers like `*`, `+`, `?`, and `{}`.

Greedy Match:
In regex, quantifiers are greedy by default. This means they will match as many occurrences of a pattern as possible.
For instance, in our regex, `+` in `([\da-z\.-]+)` and `*` in `([\/\w \.-]*)*` are greedy. They will match as much of the string as they can while still allowing the entire regex to match.

In the URL `https://www.examplesample.com/about-us`, `([\da-z\.-]+)` will match the longest sequence of characters that includes lowercase letters, digits, periods, and hyphens, which in this case would be `www.examplesample`.

Lazy Match:
A lazy or non-greedy match, on the other hand, matches as few characters as possible. It's the opposite of a greedy match.
Lazy quantifiers are denoted by adding a `?` after the standard quantifiers, like `*?` or `+?`. However, our regex does not use lazy quantifiers. In certain patterns, especially where you want to match the smallest possible part of a string, using lazy quantifiers can be very useful.

In our regex pattern, greedy quantifiers are used to find the longest matching parts for sections like the protocol, domain, top-level domain, and path of a URL. These quantifiers grab or capture as much of each part as they can, making sure we get the full and correct sections of the URL. Lazy quantifiers are not used in this pattern, which means it is set up to capture bigger and complete parts of the URL, like the whole domain name or the entire path.

### Boundaries

In the context of our regex pattern `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`, it is important to note that we do not deal with the word boundary, which is typically denoted by `\b` in regex. This specific type of boundary matches positions where a word character is followed by a non-word character, or vice versa, but it's not utilized in our current pattern. Instead, our focus is on the start `^` and end `$` string anchors, which define the boundaries of the entire string we are matching against.  These are special types of boundaries in regex that match positions rather than actual text as reviewed earlier in our Metacharacters and Anchors sections. To see how these anchors function as boundaries in relation to our sample URL `https://www.examplesample.com/about-us`, please refer to the Anchors section.


### Author

As a full-stack coding boot camp student, I am constantly exploring new technologies and techniques to broaden my development expertise. Feel free to connect with me, Helen Colon, and follow my coding journey on GitHub at https://github.com/Lychnian.
