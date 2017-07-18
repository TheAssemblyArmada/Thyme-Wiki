This file format holds most of the game strings in an encoded format that decodes to USC2 Unicode strings. The file consists of a header followed by a series of ASCII label strings and encoded Unicode strings.

### Header

```C++
enum LanguageID : int32_t
{
    LANGUAGE_ID_US,
    LANGUAGE_ID_UK,
    LANGUAGE_ID_GERMAN,
    LANGUAGE_ID_FRENCH,
    LANGUAGE_ID_SPANISH,
    LANGUAGE_ID_ITALIAN,
    LANGUAGE_ID_JAPANSE,
    LANGUAGE_ID_JABBER,
    LANGUAGE_ID_KOREAN,
    LANGUAGE_ID_CHINESE,
    LANGUAGE_ID_UNK1,
    LANGUAGE_ID_UNK2,
    LANGUAGE_ID_POLISH,
    LANGUAGE_ID_UNKNOWN,
};

struct CSFHeader
{
    uint32_t id;
    int32_t version;
    int32_t num_labels;
    int32_t num_strings;
    int32_t skip;
    LanguageID langid;
};
```

The "id" is a FourCC code that translates to the ASCII string " FSC", essentially "CSF " in little endian format.

"version" is always 3 for SAGE engine games, though the engine does check for a value of 1 or less, in which case the langid is ignored and set to 0.

"num_labels" is a count of how many string references there are in the file while "num_strings" is a count of how many encoded strings there are as each label can have more than one, though this feature is unused in SAGE games.

"skip" is a reserved 4 bytes that are unused.

"langid" corresponds to an internal enum which enumerates which language the file is intended to provide text for, though the SAGE engine games don't appear to make use of it. The provided enum is valid for Generals and Zero Hour, but not the Battle for Middle Earth games based on examination of the string files from different translations.

### Labels

```C++
struct Label
{
    uint32_t id;
    int32_t string_count;
    int32_t length;
    char label[length]
};
```

Each label consists of an "id" equivalent to the string " LBL", followed by the number of strings the label can refer to, then the length of the label ASCII string followed by the string itself. The "label" string is not null terminated and must match the given "length". The engine code refers only to the label when requesting a string for display so that localisation can be done separately.

### Strings 

```C++
struct String
{
    uint32_t id;
    int32_t length;
    uint16_t string[length]
    int32_t ex_length;         // Only present when id matches 'WRTS'
    char ex_string[ex_length]; // Only present when id matches 'WRTS'
};
```

"id" for the string is a FourCC value and must be either " RTS" or "WRTS", with "WRTS" indicating an additional ASCII string appended on. The values for the string are little endian and are encoded using a binary NOT on the value. The following is an example of how it might be decoded in C:

```C++
for (int i = 0; i < length; ++i) {
    string[i] = ~string[i];
}
```

Debug information left in certain executables suggests that the "ex_string" was related to audio files in some way, possibly as a file name for an audio file containing a reading of the string text. However it appears such a feature is not used in any SAGE game.