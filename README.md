# notationref: taxonomy of music notation concepts

This is the source code for *notationref*, a comprehensive map of music notation features across formats and software. View it here:

LINK

The goals of this project are:

* Provide a taxonomy of all Common Western Music Notation concepts, from a software developer's perspective.
* Provide a standard way for music notation software projects to document their support for each notational concept (either publicly or privately).
* Provide a web interface for viewing the taxonomy and software-specific support.

This is directly inspired by the "support tables" in websites like [MDN](https://developer.mozilla.org/en-US/) and [Can I Use](https://caniuse.com/). As those websites document web browser support for JavaScript and CSS features, notationref documents music notation software and formats' support for notational concepts.

This project is maintained by the [W3C Music Notation Community Group](https://www.w3.org/community/music-notation/), by people who have direct experience building notation software (Dorico, music21, Sibelius, Soundslice) and designing notation formats (MusicXML, SMuFL, MNX).

We created this project in order to define a to-do list for the new [MNX music notation format](https://w3c.github.io/mnx/docs/). (As such, MNX and its associated [mnxconverter utility](https://github.com/w3c/mnxconverter) are included in the tool's default view.) But beyond that affiliation, we try to avoid bias toward any particular software, format or way of thinking about music notation.

## About the taxonomy

We're under no illusion that this taxonomy is complete. In fact, it may be impossible to achieve a 100% complete taxonomy of _every_ feature of Common Western Music notation and _every_ possible way software "thinks" about music.

But with that said, there _is_ a lot of value in this taxonomy, even if it can never be complete. It's very handy for developers of music notation software, to give them an effective to-do list or simply serve as a reminder of what notations they might choose to support. It's also handy in creating internal software documentation.

We very happily accept contributions to the taxonomy. Pull requests welcome!

## Technical details

The taxonomy is defined as a hierarchical JSON data structure in concepts.json. Each object has a `"type"` (`"group"`, `"subgroup"` or `"item"`). Each `"item"` defines a simple ID string: for example, `"event-staccato"` for a staccato marking.

Each "format" (such as MNX) is also defined as a JSON file. It's a simple object with these keys:

* `"name"`: The format/software name
* `"infoUrl"`: A URL for information about the format/software
* `"support"`: A dictionary mapping concept ID strings to support information

Support information is a dictionary with these keys:

* `"level"`: A number specifying this format's support for the concept. `1` means supported; `2` means partially supported; `3` means unsupported.
* `"text"`: Text that describes this format's support.
* `"link"`: An optional URL with more information (e.g., a deep link to specific documentation)

Have a look at formats/mnx.json for a working example.

The design is deliberately decoupled, so that format JSON files do not need to live in this git repository.

## Adding your own software or notation format

To document your own software/format, copy the file `formats/empty.json` from this repo and fill in the information for each notational concept.

When you're done, publish that JSON file somewhere on the web. We plan to improve the tool to allow for importing arbitrary JSON URLs (coming soon), at which point you'll be able to load your software/format. (For the time being, feel free to hack a local copy of index.html to load your custom JSON file instead of mnx.json.) We also plan on hosting a simple list of publicly available format JSON files.

Note: we encourage developers to create separate format files for different aspects of their software. Music notation applications are complex, and in practice it's possible for them to support some notations in _some_ cases but not in others.

For example, here are the files Soundslice uses to document its feature support internally:

* Rendering engine support ("Can the graphics engine draw this notation?")
* Editor support ("Does the notation editor allow for adding/changing/deleting this notation?")
* MusicXML importer support ("Does the MusicXML importer import this notation?")
* MusicXML exporter support ("Does the MusicXML exporter export this notation?")
* MIDI exporter support ("Does the MIDI exporter export this notation?")
* OMR support ("Does the OMR engine detect this notation?")
