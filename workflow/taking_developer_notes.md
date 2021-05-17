Taking Developer Notes
================================================================================

2021-05-15 Sat

Contents
--------------------------------------------------------------------------------

* Types of Notes [tNoteTypes]
  - Handwritten
  - Lab Book - Markdown
  - Notes/Development - Markdown
  - Job/Ticket Status - Markdown
  - Personal - Markdown
  - TIL - Markdown
  - Blog - Markdown
  - Hourly Logs - Handwritten or Markdown
* Hourly Logs - Handwritten Vs Markdown [tLogsMethod]
* Debugging and Optimizing [tDebugging]
  - Strategy [tDebuggingStrategy]
  - What to record [tDebuggingWhat]
  - Tools [tDebuggingTools]
* My Method [tMyMethod]


Types of Notes: Handwritten & Markdown [tNoteTypes]
--------------------------------------------------------------------------------

* Handwritten
* Lab Book - Markdown
* Notes/Development - Markdown
* Hourly Logs - Markdown
* Job/Ticket Status - Markdown
* Personal - Markdown
* TIL - Markdown
* Blog - Markdown

### Handwritten

* Daily TODO
* Working memory/reminders to refer back to throughout day
* Activity notes
* Meeting notes
* Development plans
* Debugging and optimization hypothesis 

### Lab Book - Markdown

* Experiments/development/debugging steps:
  - What to test and expected results
  - Actual code, terminal commands, settings, screenshits
  - Output/results
  - repeat

### Notes/Development - Markdown

* Background info for development topics
  - How to connect with 3rd party services
  - How app domains interact
* Procedures, steps 
  - How to log into services
* Code snippets 
  - Specific code@ to copy and paste

### Job/Ticket Status - Markdown

* Important to have as a Historical record and for sharing
* Keep a running log, moving each job from one week to the next until it's done
* Also keep a static historical snapshot of each week's log
* Each ticket gets its own section with:
  - Description
  - Current status
  - Status: in progress, needs approval, merged, blockers
  - Log: any notable events

### Personal - Markdown

* Individual markdown files for topics like education goals and tracking

### TIL - Markdown

* Today I Learned (TIL): Summaries and references for important topics

### Blog - Markdown

* More formalized writings than TIL, but could take inspiration from TIL

### Hourly Logs - Handwritten or Markdown

Source: https://www.lifehack.org/articles/productivity/how-logging-your-day-can-lead-to-higher-effectiveness.html
source: https://zapier.com/blog/productivity-journal/

* Purpose:
  - Improves performance effectiveness through awareness of:
    - How long it took to do something
    - Issues encountered
    - Deciding what to do next
    - Estimate how long an activity could take
    - Determine which activities need to be cut
  - Reminders of what has or has not been done on a topic when you're speaking
    to someone
  - Content for documentation when needed
* What: Time and date of:
  - Actions performed
  - Topics learned
  - Issues to keep an eye on throughout day
* When:
  - Interstitial journaling - every time you switch from one task to another,
    note the time. Even if it's a subtask and the main task isn't complete
  - Daily Summary - Just once or twice a day record the larger completed tasks
    without needing to dive into the details. This can give you an overview of
    how long it takes to complete a task including the average interruptions
    along the way.
* Record Why:
  - Include not just "what", but also **"why"** something was done
  - A reminder to what caused the action to happen
  - A reminder to why something took longer/shorter than expected
  - Helps determine if the activity was important and if it should be repeated
    or avoided
* Review regularly to maintain awareness and discover TODO items
* See [tLogsMethod] for pros and cons of Handwritten Vs Digital Hourly Logs


Hourly Logs - Handwritten Vs Digital [tLogsMethod]
--------------------------------------------------------------------------------

source: https://www.lifehack.org/895443/log-daily-activities
source: https://zapier.com/blog/productivity-journal/

### Handwritten

* A notebook and pens is much more accessible than an app/computer file that
  must be opened. If you already have your computer open then that's not
  difficult, but for the times when you don't it adds friction.
* More free-form - easier to draw boxes and arrows to connect ideas
* Handwriting is a more focused process

### Digital Computer File

* Easier to archive and search
* Entry is faster and timestamps can be automated
* Easier if you're already at a computer so you don't need to switch
  context/move your keyboard or shift body to open a paper notebook
* There's no need to transcribe the notes to a digital archive for storage and
  makes updating Status report logs easier since it can be copy and pasted


Debugging and Optimizing [tDebugging]
--------------------------------------------------------------------------------

### Strategy [tDebuggingStrategy]

Debugging involves gathering data and testinng hypothesis. The key is to take
notes along the way. This prevents you from repeating what you've already done,
staying focusing on original hypothesis, and when you do get stuck there is
documentation of what has already been tried.

This also makes it a lot easier to communicate with others when you need help.

Use a pseudo Scientific Method:

1. Hypothesis of possible causes and possible fixes
2. Formulate tests or write some code to solve the problem (take notes!)
3. Tweak hypothesis based on outcomes
4. Repeat

Recci

Making code changes and recording the results:

1. Save the output of `history`
2. Make commits to test branches
3. Record the correlatoin between them

source: https://blog.nelhage.com/2010/05/software-and-lab-notebooks/ 

### What to record [tDebuggingWhat]

* Commands/Actions: code, terminal commands, settings
  - `fc`, `pbcopy`, `pbpaste`
* Text Output
* Screenshots

### Tools [tDebuggingTools]

* `fc`: To retrieve command-line history to record, and compose new commands

```
# Examples:
# After editing, saving, and exiting the editor, the command will execute
fc # edit last command
fc -lf # list history with date/time
fc -lf 15 # list history from a specified line number and later
fc -lf -5 # list history of last 5 lines
fc 15 20 # edit range of line numbers
fc -e - 15 20 # edit range of line numbers
# <ctrl-r> interactive searchable list of past commands
```


My Method [tMyMethod]
--------------------------------------------------------------------------------

I use most of the types listed in the "Types of Notes" section. For
Logs I handwrite "Interstitial" logs throughout the day and then summarize the
tasks in a "Daily Summary" markdown file. I transfer the ticket-specific
summary notes to the corresponding ticket summary in the Status markdown file.

This is a lot of effort but I haven't decided yet which types of notes are most
useful and which I can do without.
