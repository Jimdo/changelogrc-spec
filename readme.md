.changelogrc-spec
=================

There are multiple tools that work with commit message formats
to generate changelogs and releases, provide help by writing
good commit messages, lint your messages and many more (to come).

Although conceptual similar all these tools need to be configured
individually which adds an unnecessary overhead to tooling setup.


Spec
----

1. ### File
	1. Custom configuration for changelog/commit formats __CAN__ be placed
	   in a `.changelogrc` file.
	2. A `.changelogrc` file __MUST__ be formatted as JSON.
	3. Tools __MUST__ search all parent directories of the current working
	   directory for a `.changelogrc` file.

2. ### Inheritance
	1. The `.changelogrc` file closest to the current working directory
	   __MUST__ be used for configuration.
	2. `.changelogrc` files __MUST NOT__ be merged with `.changelogrc` 
	   files in parent directories unless specified by the `.changelogrc`
	   itself (see 5.i.).

3. ### Types
	1. A `.changelogrc` file __CAN__ provide an array of change "types".
	2. A type __MUST__ specify a "key" with which a commit may be identified
	   as the type.
	3. A type __SHOULD__ specify a "name" as a human readable reference to
	   the type "key".
	4. A type __CAN__ provide "hide" attribute, specifying if this type
	   should occur in human readable formats or not.

	example `.changelogrc` with types:

	```json
	{
		"types": [
			{
				"key": "feat",
				"name": "Features"
			},
			{
				"key": "test",
				"name": "Tests",
				"hide": true
			}
		]
	}
	```

4. ### Notes
	1. A `.changelogrc` file __CAN__ provide an array of change "notes".
	2. A note __MUST__ specify a "keyword" with with a commit is identified
	   as containing this note.
	3. A note __CAN__ specify an array of "alias"-es that serve as alternative
	   "keywords".
	4. A note __CAN__ provide a "important" attribute, specifying this change
	   as important.
	5. Important notes (see 4.iv.) __MUST__ invalidate the hide attribute of 
	   types (see 3.iv.).  
	   *[An important note __MUST NOT__ be hidden.]*

	example `.changelogrc` with note:

	```json
	{
		"notes": [
			{
				"keyword": "BREAKING CHANGES",
				"alias": [
					"BREAKING CHANGE"
				],
				"important": true
			}
		]
	}
	```

5. ### Extend
	1. A `.changelogrc` file __CAN__ provide an "extend" property specifying
	   a path to another `.changelogrc` file in with the configuration is
	   deeply merged.


License
-------

> The MIT License
> 
> Copyright (C) 2016 Jimdo GmbH
> 
> Permission is hereby granted, free of charge, to any person obtaining a copy of
> this software and associated documentation files (the "Software"), to deal in
> the Software without restriction, including without limitation the rights to
> use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies
> of the Software, and to permit persons to whom the Software is furnished to do
> so, subject to the following conditions:
> 
> The above copyright notice and this permission notice shall be included in all
> copies or substantial portions of the Software.
> 
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
> IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
> FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
> COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
> IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
> CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
