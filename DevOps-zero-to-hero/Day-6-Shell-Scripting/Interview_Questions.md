### Crucial DevOps Interview Questions Discussed in these Lectures

When you interview for a DevOps Internship, hiring managers will pull real scenarios from these classes. Here are the core conceptual questions you must memorize:

#### Q1: What happens if a command fails in the middle of a Bash script execution? How do you gracefully protect production operations against this?
* **Answer:** By default, Bash continues running downstream commands even if an earlier step fails completely. To change this behavior, we configure `set -e` at the start of our code. This tells the interpreter to drop execution immediately if any independent command produces a non-zero exit code.

#### Q2: What is the limitation of `set -e` when using pipes (`|`), and how does `set -o pipefail` fix it?
* **Answer:** If you use a pipe like `command1 | command2`, `set -e` only looks at the exit status of the *very last* command (`command2`). If `command1` crashes but `command2` succeeds, the script falsely treats the step as successful. Adding `set -o pipefail` forces Bash to monitor the entire pipeline. If any individual part of the pipeline fails, the whole script stops.

#### Q3: How do you extract and print specific columns of data from log output using the terminal?
* **Answer:** We combine pipelines (`|`) with text filtering utilities like `awk` and `grep`. We use `grep` to filter down to the specific lines we want, and then pass that text into `awk '{print $X}'` (where `X` represents the column position) to isolate and print the exact data field needed.