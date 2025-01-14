# jsmest

Generates tests using a question bank. Reads from a JSON string and generates both a printable version and Moodle XML. A grading schema is also proposed, as well as an Excel formula.

The following question types are supported:
- Multiple choice
- Short answer (2+2=?)
- Essay (Write a program...)

Questions are grouped into categories.

Each question object in the JSON can be replaced with an array of questions.

The number of answers of a multiple choice question is limited to 4.

Multiple variants can be generated from the same question bank.

The idea is based on Milo Sredkov's MEST tool.

Sample JSON input:

```
[
	{
		"type": "closed",
		"category": "intro",
		"year": 2020,
		"title": "2 + 2 = ?",
		"correct": ["4", "four"],
		"wrong": ["3", "1"]
	},
	[
		{
			"type": "closed",
			"category": "for",
			"year": 2020,
			"title": "Which of the following is correct?",
			"correct": ["A for-loop is...", "..."],
			"wrong": ["A for-loop cannot be inifinite", "..."]
		},
		{
			"type": "closed",
			"category": "for",
			"year": 2020,
			"title": "Which of the following is NOT correct?",
			"correct": ["A for-loop is...", "..."],
			"wrong": ["...", "..."]
		}
	],
	((a) => eval(
		{
			"type": "short-open",
			"category": "if",
			"year": 2020,
			"title": `What's the output of the following code: <code>int a =${a}; cout &lt;&lt; a * 10 + 43;</code>`,
			"correct": `${a}43`
		}))(Math.floor(Math.random() * 9 + 1)),
	{
		"type": "long-open",
		"category": "functions",
		"year": 2020,
		"title": "Write a function...",
		"correct": "int myAwesomeFunction(double x, double y) ..."
	}
]
```

