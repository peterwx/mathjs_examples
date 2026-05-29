# Index

${toc}

++Introduction++:

Information mostly obtained from Joplin's(Android) menu/view Configuration -> Tools -> SYNC STATUS screen/view after normal/traditional or AI OCR text content extraction on a scrolling screenshot(by tapping scroll button on a taken screenshot) copied to and OCR'ed by Keep(Google) through its grab image text feature, for example.

- First installation ever(on Android OS) around 2024-08-21.
- 540 h. usage in 2025.

# Status

Last obtained on 2025-11-05.

++Attachments++:

Not downloaded: 0
Downloading: 0
Downloaded and decrypted: 0
Downloaded and encrypted: 0
Created locally: 143
Error: 0

++Sync status (synced items / total items)++:

Note=425/425
Folder=72/72
Resource=143/143
Tag=14/14
NoteTag=89/89
Revision=661/661
Total=1404/1404
Conflicted=0
To delete=0

++Synced items++:
=sum([425,72,143,14,89,661])

++Total items++:
=sum([425,72,143,14,89,661])

++Average tag note count++:
=round(89/14, 2)

++Resources or attachments percentage of notes count++:
=round(143*100/425, 2)

## Folder statistics

Folder statistics presented next don't include their immediate(children) and nested subfolders statistics or note counts. Statistics values obtained from the math code block calculations in the next section(Notebooks).

| ++Statistic name++       | ++Statistic value++ |
| :----------------------: | :-----------------: |
| Note count               | 425                 |
| Folder count             | 72                  |
| Avg. notes per folder    | 5.9                 |
| Empty folders            | 17                  |
| Folders w/ single note   | 10                  |
| Folders w/ two notes     | 11                  |
| Median folder note count | 2                   |

## Notebooks

```math
//createUnit('note', {aliases: ['notes']})

isZero(x)= x == 0
isOne(x)= x == 1
isDouble(x)= x == 2

# To note that deleted folders(now in trash folder) are included in the folders list, with those that are non empty contributing to the note total. Directly deleted notes(placed at Thrash folder root level) don't get added or counted toward the notes total,

expressions=[AIDialogues=0,Android=3,ATestBook=0,ATestSubBook=1,Body=6,Bookmarklets=2,Catalogs=0,ChatGPT=0,Chores=5,Claude=2,Coding=1,Comparisons=8,Components=0,Computing=2,Configurations=0,Contacts=6,Cooking=13,DesktopApps=3,Devices=0,Diagrams=5,Dossiers=2,Editors=0,Extensions=0,Extensions=2,Firefox=3,Gemini=0,Glossaries=1,Hardware=4,Houses=2,Humor=48,Indexes=7,Joplin=17,JoplinDesktop=0,Linux=1,Logs=1,Main=15,Manuals=0,MarkdownShowcase=0,MathJSExamples=9,MobileApps=12,Monetary=4,NotationsMath=2,OtherChromium=4,Owned=8,Perplexity=2,Personal=1,Phrases=30,Platforms=0,Poems=2,Python=4,PythonScripts=2,Quotes=12,References=1,Relax=3,Rural=12,ScanResultsPC=0,Security=1,Smartphone=36,Software=8,Steam=2,Storage=0,Texts=11,Thoughts=40,TODOS=15,Tour=5,Transport=5,Vivaldi=8,Vivaldi=0,Web=5,Welcome=1,Windows=19,Writings=1]
labels= size(expressions)
//Note count
sum(expressions)
// Average notes per folder
mean(expressions)
empty= size(filter(expressions, isZero))[1]
single= size(filter(expressions, isOne))[1]
double= size(filter(expressions, isDouble))[1]
median(expressions)

```
