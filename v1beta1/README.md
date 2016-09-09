# Speech Recognition Script for Asterisk

These example shows how to use the [Google Cloud Speech API][speech-api] to render speech
to text and return it back to the dialplan as an Asterisk channel variable.

**This source code is different from the original version:**

- [ ] The Perl Programming Language
- [x] The **Python** Programming Language

## Requirements

- [Python](https://www.python.org/) - The Python Programming Language
- [pyst2](https://github.com/rdegges/pyst2) - Python Libraries for Asterisk
- [Google Cloud Speech REST API](https://github.com/GoogleCloudPlatform/python-docs-samples/tree/master/speech/api-client)
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

Follow the installation instructions on the [Google Cloud Speech REST API](https://github.com/GoogleCloudPlatform/python-docs-samples/tree/master/speech/api-client) page.

`pip install -r requirements.txt`

----

## Usage
`agi(speech-recog.agi)`

### Examples

sample dialplan code for your extensions.conf

```
;Simple speech recognition
exten => 1234,1,Answer()
 same => n,agi(speech-recog.agi)
 same => n,Verbose(1,The text you just said is: ${RESPONSE})
 same => n,Hangup()
```

-------------------
Supported Languages
-------------------
[['Afrikaans',       ['af-ZA']],
 ['Bahasa Indonesia',['id-ID']],
 ['Bahasa Melayu',   ['ms-MY']],
 ['Català',          ['ca-ES']],
 ['Čeština',         ['cs-CZ']],
 ['Deutsch',         ['de-DE']],
 ['English',         ['en-AU', 'Australia'],
                     ['en-CA', 'Canada'],
                     ['en-IN', 'India'],
                     ['en-NZ', 'New Zealand'],
                     ['en-ZA', 'South Africa'],
                     ['en-GB', 'United Kingdom'],
                     ['en-US', 'United States']],
 ['Español',         ['es-AR', 'Argentina'],
                     ['es-BO', 'Bolivia'],
                     ['es-CL', 'Chile'],
                     ['es-CO', 'Colombia'],
                     ['es-CR', 'Costa Rica'],
                     ['es-EC', 'Ecuador'],
                     ['es-SV', 'El Salvador'],
                     ['es-ES', 'España'],
                     ['es-US', 'Estados Unidos'],
                     ['es-GT', 'Guatemala'],
                     ['es-HN', 'Honduras'],
                     ['es-MX', 'México'],
                     ['es-NI', 'Nicaragua'],
                     ['es-PA', 'Panamá'],
                     ['es-PY', 'Paraguay'],
                     ['es-PE', 'Perú'],
                     ['es-PR', 'Puerto Rico'],
                     ['es-DO', 'República Dominicana'],
                     ['es-UY', 'Uruguay'],
                     ['es-VE', 'Venezuela']],
 ['Euskara',         ['eu-ES']],
 ['Français',        ['fr-FR']],
 ['Galego',          ['gl-ES']],
 ['Hrvatski',        ['hr_HR']],
 ['IsiZulu',         ['zu-ZA']],
 ['Íslenska',        ['is-IS']],
 ['Italiano',        ['it-IT', 'Italia'],
                     ['it-CH', 'Svizzera']],
 ['Magyar',          ['hu-HU']],
 ['Nederlands',      ['nl-NL']],
 ['Norsk bokmål',    ['nb-NO']],
 ['Polski',          ['pl-PL']],
 ['Português',       ['pt-BR', 'Brasil'],
                     ['pt-PT', 'Portugal']],
 ['Română',          ['ro-RO']],
 ['Slovenčina',      ['sk-SK']],
 ['Suomi',           ['fi-FI']],
 ['Svenska',         ['sv-SE']],
 ['Türkçe',          ['tr-TR']],
 ['български',       ['bg-BG']],
 ['Pусский',         ['ru-RU']],
 ['Српски',          ['sr-RS']],
 ['한국어',            ['ko-KR']],
 ['中文',             ['cmn-Hans-CN', '普通话 (中国大陆)'],
                     ['cmn-Hans-HK', '普通话 (香港)'],
                     ['cmn-Hant-TW', '中文 (台灣)'],
                     ['yue-Hant-HK', '粵語 (香港)']],
 ['日本語',           ['ja-JP']],
 ['Lingua latīna',   ['la']]];

-----------------------
Security Considerations
-----------------------
This script contacts googles' servers in order send the recorded voice data and get back
the resulted text. The script uses SSL by default to encrypt all the traffic between
your pbx and google servers so no 3rd party can eavesdrop your communication, but your
voice data will be available to Google under a not yet defined policy.

------------
Tiny version
------------
The '-tiny' suffixed scripts use the HTTP::Tiny perl module instead of LWP::UserAgent and
JSON::Tiny instead of JSON. This makes them a lot faster when run in small embedded systems
or boards like the Raspberry pi. They can be used as an in-place replacement of the normal
scripts and expose the same interface/cli args. To use them just make sure
you have HTTP::Tiny and JSON::Tinyinstalled.

-------
License
-------
The speech-recog script for asterisk is distributed under the GNU General Public
License v2. See COPYING for details.

--------
Homepage
--------
http://zaf.github.com/asterisk-speech-recog/
