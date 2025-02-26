
bashFile.sh

# scripting

#!/bin/bash

set -e - will stop on error.
set +e normal state (disable set -e)

-eq ==
-ne <>
-lt <
-le <=
-gt >
-ge >=

> /dev/null - send output to null
(ls > /dev/null)

2> /dev/null - send error to null
(ls nonexistent_directory 2> /dev/null)

Discarding Both Standard Output and Standard Error
2>&1
(command > /dev/null 2>&1)
