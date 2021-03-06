# OctoPrint-DetailedProgress

A plugin that sends M117 (and optionally M73) commands to the printer to display the progress of the print job being currently streamed. The message to display can be configured (some placeholders included).
![Example ETA](https://i.imgur.com/ocBp152.jpg)
![Example ETL](https://i.imgur.com/oJiMm2p.jpg)
![Example Percent](https://i.imgur.com/McaCNsx.jpg)
![Example M73 Prusa](https://i.imgur.com/C1zeANH.jpg)

## Setup

Install manually using this URL:

    https://github.com/tpmullan/OctoPrint-DetailedProgress/archive/master.zip

## Configuration

### Manual Config File
``` yaml
plugins:
  detailedprogress:
    # Number of seconds (minimum) to rotate the messages
    time_to_change: 10
    eta_strftime: "%H:%M:%S Day %d"
    etl_format: "{hours:02d}:{minutes:02d}:{seconds:02d}"
    # Send M73 progress commands 
    use_M73: true
    # M73 commands syntax specific for Prusa Firmware (>=3.3.0)
    M73_PrusaStyle: true
    # Messages to display. Placeholders:
    # - completion : The % completed
    # - printTime : A string in the format "HH:MM:SS" with how long the print is going
    # - printTimeLeft : A string in the format "HH:MM:SS" with how long the print still has left
    # - ETA : The date and time formatted in "%H:%M:%S Day %d" that the print is estimated to be completed
    # - filepos: The current position in the file currently being printed
    # - filename: The filename of file currently being printed
    # - accuracy: Accuracy of the time estimates
    messages:
      - "{completion:.2f}% complete"
      - "ETL: {printTimeLeft}"
      - "ETA: {ETA}"
    print_done_message: "Print Done"
```
### Plugin Settings menu

![Example Settings](https://i.imgur.com/wdFGGrN.jpg)

### Time Variables:

* The eta_strftime uses built in python functions to format the time, examples can be found [here](https://strftime.org/).  
* Be careful when using the character `:` in the messages, some firmwares will [expect a checksum and crash](https://community.octoprint.org/t/error-no-checksum-with-line-number-last-line-18/8838/2).  To fix this issues either omit the character or update to the latest version of Marlin.
