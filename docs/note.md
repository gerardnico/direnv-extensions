This script was originally entirely written by Claude 3.5 Sonnet
Prompt:
Can you write a bash script that:
* will get an env file as first argument called the `input` variable
* create an `output` variable
* start a loop to go through each line of the `input` file,
* filter out  all comments (line that starts with a #),
* separate the key from the value in 2 variables called respectively `key` and `value`
* if the value starts with `secret`
  * get the remaining text in a variable called `secret_path`
  * make a hashicorp `vault` call to a key value store to get the value where the path is the value of the `secret_path` variable
  * store the value in the `value` variable
* add to the `output` variable the line  `export $key=$value`
* once the loop has finished, echo the whole `output` variable