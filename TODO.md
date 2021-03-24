# To-do Checklist

Need to incorporate package.json 'keys & values' into my config.yml file.
- reference in the YAML script where the package.json file is
- write a script which specifically uses and targets the JSON keys & values.

## TODOs: NPM Access Error

npm ERR! code EACCES
npm ERR! syscall access
npm ERR! path /usr/local/lib/node_modules/npm/node_modules/abbrev
npm ERR! errno -13
npm ERR! Error: EACCES: permission denied, access '/usr/local/lib/node_modules/npm/node_modules/abbrev'
npm ERR!  [Error: EACCES: permission denied, access '/usr/local/lib/node_modules/npm/node_modules/abbrev'] {
npm ERR!   errno: -13,
npm ERR!   code: 'EACCES',
npm ERR!   syscall: 'access',
npm ERR!   path: '/usr/local/lib/node_modules/npm/node_modules/abbrev'
npm ERR! }
npm ERR! 
npm ERR! The operation was rejected by your operating system.
npm ERR! It is likely you do not have the permissions to access this file as the current user
npm ERR! 
npm ERR! If you believe this might be a permissions issue, please double-check the
npm ERR! permissions of the file and its containing directories, or try running
npm ERR! the command again as root/Administrator.

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/circleci/.npm/_logs/2021-03-23T01_09_48_242Z-debug.log

Exited with code exit status 243

## NPM unable to find file or directory

npm ERR! code ENOENT
npm ERR! syscall open
npm ERR! path /home/circleci/project/package.json
npm ERR! errno -2
npm ERR! enoent ENOENT: no such file or directory, open '/home/circleci/project/package.json'
npm ERR! enoent This is related to npm not being able to find a file.
npm ERR! enoent 

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/circleci/.npm/_logs/2021-03-23T01_09_49_758Z-debug.log

Exited with code exit status 254

## No artifact files found

Uploading /home/circleci/project/outputs/sast to outputs/sast/
  No artifact files found at /home/circleci/project/outputs/sast