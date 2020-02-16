# Mkdocs publishing workflow


I write articles on my personal computer.

Markdown has some great advantages : 

- stored as plain text on disk
- content is indexed making it easy to find content with Alfred/Spotlight/grep
- you can grep, sed, awk the hell out of them and bring corrections very quickly
- can be stored in a Git repository

This is my current publication workflow:

- I edit articles locally with [Visual Studio Code] (yes, it is an open source Microsoft product, and it is very good)
- I commit changes to my [GitHub] 
- With an Alfred workflow, I connect to my VPS and do:
    - a "git pull" to retrieve updates
    - rebuild the doc (which is served as static files by the HTTP server)
- Article is online