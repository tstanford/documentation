# Vim Reference Guide

Tim Stanford

## Different Modes

|     Mode      |   Description                                                                                |
|---------------|----------------------------------------------------------------------------------------------|
|  Normal       |  Hit Escape to switch to Normal Mode, Default. For Navigation and simple editing             |
|  Insert       |  Hit i to switch to Insert Mode, Explicitly inserting and modifying of texts                 |
|  Command Line |  Hit Esc then press : to switch to Command Line Mode. Operate Vim live Saving, Exiting, etc   |


## Opening, Closing and Saving File

|    Command    |   Description                            |
|---------------|------------------------------------------|
| vim File_Name | Create of modify a FILE_NAME in Vim      |
| :q! or :ZQ    | Exit Vim without saving the current file |
| :x! or :wq!   | Save the current file and exit           |


## Basic Navigation

|    Command    |   Description                                                                                             |
|---------------|-----------------------------------------------------------------------------------------------------------|
| :set number   | Turn on line visual line numbering.                                                                       |
| :LINE_NUMBER  | Jump to LINE_NUMBER, where it is a numeric number representing the to navigate to. Perform in Command mode|
| :$            | Jump to the last line. Perform in Command mode                                                            |
| $             | Jump to end of current line. Perform in Normal mode                                                       |
| G             | Jump to the last line. Perform in Normal mode                                                             |
| nG            | Jump to the n line. Where n is the line number. Perform in Normal mode                                    |


## Basic Editing (Perform in Normal Mode)

|    Command    |   Description                                                                  |
|---------------|--------------------------------------------------------------------------------|
|  dd           |   Delete the highlighted or the current line.                                  |
|  v            |   Highlight the text. Move left and right arrows to extend or to reduce        |
|  y            |   Yank/Copy the highlighted text or the current line                           |
|  p            |   Paste the previously copied text                                             |
|  o            |   Go into insert mode and add a new line after the cursor                      |
|  a            |   move cursor to the right and enter insert mode                               |
|  A            |   move to end of line and enter insert mode                                    |
|  s            |   go into insert mode and delete current character under cursor                |


## Basic Searching

|    Command          |   Description                                                                  |
|---------------------|--------------------------------------------------------------------------------|
|  :/SEARCH_KEYWORD   |   Jump to the text matching SEARCH_KEYWORD. Perform in command mode            |
|  n                  |   Jump to the next match                                                       |
|  :noh               |   Clear the current search. Perform in command line mode                       |

## Split Mode

|    Command          |   Description                                                                  |
|---------------------|--------------------------------------------------------------------------------|
|  :split FILE_NAME   |   Horizontally open another file names FILE_NAME when a file is already open   |
|  :vsplit FILE_NAME  |   Vertically open another file names FILE_NAME when a file is already open     |
|  CTRL ww            |   Switch between windows in split view. Perform in normal mode                 |

## Editing Multiple files

|    Command          |   Description                                                                  |
|---------------------|--------------------------------------------------------------------------------|
| vim File_Name1 File_Name1 | Open vim in multiple file mode. First file to edit is File_Name1
|  :n                 |   move to next file |
|  :N                 |   move to previous file |

## Options

|    Command          |   Description                                                                  |
|---------------------|--------------------------------------------------------------------------------|
|  :set nowrap        |   Turn off line wrapping |
|  :set wrap          |   Turn on line wrapping |



Selection

vi'     select text inside single quotes
vi"     select text inside double quotes
viB     select inside block { }
