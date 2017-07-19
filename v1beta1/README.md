# Speech Recognition Script for Asterisk

These example shows how to use the [Google Cloud Speech API][speech-api] to render speech
to text and return it back to the dialplan as an Asterisk channel variable.

**This source code is different from the original version:**

- [ ] The Perl Programming Language
- [x] The **Python** Programming Language

## Requirements

- [Python](https://www.python.org/) - The Python Programming Language
- [pyst2](https://github.com/rdegges/pyst2) - Python Libraries for Asterisk
- [Google Cloud Speech REST API](https://github.com/GoogleCloudPlatform/python-docs-samples/tree/master/speech/cloud-client)
  - [Cloud Speech API Account & Credentials](https://console.cloud.google.com)
- Internet access in order to contact google and get the speech data.

----

## Installation

To install, copy speech-recog.agi to your agi-bin directory.  

Usually this is /var/lib/asterisk/agi-bin/

To verify the AGI Scripts directory check /etc/asterisk/asterisk.conf or Asterisk settings:

`Asterisk*CLI> core show settings`

### pyst2

To install pyst2, simply run:

`pip install pyst2`

This will install the latest version of the library automatically.

  - pyst2 support ASCII by default.

### Google Cloud Speech REST API

Follow the installation instructions on the [Google Cloud Speech REST API](https://github.com/GoogleCloudPlatform/python-docs-samples/tree/master/speech/cloud-client) page.

`pip install -r requirements.txt`

----

## Usage
`agi(speech-recog.agi)`

### Examples

sample dialplan code for your extensions.conf

```
; ~ Simple speech recognition
exten => 1234,1,Answer()
 same => n,agi(speech-recog.agi)
 same => n,Verbose(1,The text you just said is: ${RESPONSE})
 same => n,Hangup()
```

## Supported Languages

See [Language Support](https://cloud.google.com/speech/docs/best-practices#language_support) for a list of the currently supported language codes. 


## Security Considerations

This script contacts googles' servers in order send the recorded voice data and get back
the resulted text. The script uses SSL by default to encrypt all the traffic between
your pbx and google servers so no 3rd party can eavesdrop your communication, but your
voice data will be available to Google under a not yet defined policy.

## License

```text
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

## Homepage

http://zaf.github.com/asterisk-speech-recog/
