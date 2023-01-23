# simple bash scritps

Could you prepare bash scripts with arguments like env, path, tags?  Please follow next requirements:
- use switch case and process all arguments by while but without getopts function.
- add help options and functions with simple descriptions.
- add check for arguments  if it is less the count of arguments return 1


Results:

```
#!/bin/bash

# Function to display help message
display_help() {
  echo "Usage: $0 [options]"
  echo
  echo "Options:"
  echo "  -e, --env   Specify environment (dev, staging, prod)"
  echo "  -p, --path  Specify path (default is /tmp)"
  echo "  -t, --tags  Specify tags (comma separated list)"
  echo "  -h, --help  Display this help message"
}

# Define default values
env="dev"
path="/tmp"
tags=""

# Process command line arguments
while [[ $# -gt 0 ]]
do
  key="$1"
  case $key in
    -e|--env)
      env="$2"
      shift
      ;;
    -p|--path)
      path="$2"
      shift
      ;;
    -t|--tags)
      tags="$2"
      shift
      ;;
    -h|--help)
      display_help
      exit 0
      ;;
    *)
      echo "Invalid option: $key"
      display_help
      exit 1
      ;;
  esac
  shift
done

# Check if count of arguments is less
if [[ $# -lt 3 ]]; then
  echo "Missing arguments"
  display_help
  exit 1
fi

# Your script logic goes here
echo "Environment: $env"
echo "Path: $path"
echo "Tags: $tags"
```

example usage
```
./script_name -e production -p /home/project -t tag1,tag2
```