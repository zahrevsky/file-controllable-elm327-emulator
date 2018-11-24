python-ELM
==========

A python simulator for the ELM327 OBD-II adapter. Built for testing [python-OBD](https://github.com/brendanwhitfield/python-OBD).

This simulator can process basic examples in [*python-OBD* documentation](https://python-obd.readthedocs.io/en/latest/) and reproduces a limited message flow
generated by a Toyota Auris Hybrid car, including some custom messages.

Run with:

```shell
python -m elm
```

Tested with python 3.7.

The serial port to be used by the application interfacing the simulator is displayed in the first output line. E.g.,:

    Running on /dev/pts/1

Logging is controlled through `elm.yaml` (in the current directory by default). Its path can be set through the *ELM_LOG_CFG* environment variable.

A dictionary is used to define commands and pids. The dictionary includes more sections:

- `'AT'`: AT commands
- `'default'`: all default pids
- any additional custom section can be used to define specific scenarios

If `emulator.scenario` is set to a string different from *default*, the custom scenario set by the string is applied; any key defined in the custom scenario replaces the default settings ('AT' and 'default' scenarios).

Allowed keys to be used in the dictionary:

- `'Pid'`: short pid description
- `'Descr'`: shall be set to a string describing the pid
- `'Exec'`: command to be executed
- `'Log'`: logging.debug argument
- `'ResponseFooter'`: run a funtion and returns a footer to the response
- `'ResponseHeader'`: run a funtion and returns a header to the response
- `'Response'`: returned bytes 
- `'Action'`: can be set to 'skip' in order to skip the processing of the pid
- `'Header'`: not used

At the *Enter command:* prompt, the emulator accepts the following commands:

- `q` = quit
- `p` = pause
- `r` = resume
- `emulator.scenario='name of the new scenario'`
- any other Python command can be used to query/configure the backend thread
