# Datatypes

[INDEX](../../README.md)

## Overview
Puppet language involve some form of data. An individual piece of data is called a value, and every value has a data type, Strings are the most common and useful data type.

### Abstract data types
You can use one of the abstract data types to construct a data type that suits your needs.

#### Optional data type: 

- Examples:
  - Optional[String]: Matches any string or undef.
  - Optional[Array[Integer[0, 10]]]: Matches an array of integers between 0 and 10, or undef.
  - Optional["present"]: Matches the exact string "present" or undef.

#### NotUndef data type:
matches anything except undef.

#### Variant data type:

- Examples:
  - Variant[Integer, Float]: Matches any integer or floating point number (equivalent to Numeric).
  - Variant[Enum['true', 'false'], Boolean]: Matches 'true', 'false', true, or false.

#### Enum data type:

- Examples:
  - Enum['stopped', 'running']: Matches the strings 'stopped' and 'running', and no other values.
  - Enum['true', 'false']: Matches the strings 'true' and 'false', and no other values. Does not match the boolean values true/false.

### Arrays:
```python
# Generic array witn String elements
Array[String]

# Generic Array with any type of elements and 5 minimun objects
Array[Any, 5]

# Generic Array with any type of elements between 5 and 10 objects
Array[Any, 5, 10]

# Examples
[ 'one', 'two', 'three' ]
# Equivalent:
[ 'one', 'two', 'three', ]

$my_array = [ 'one', 'two', 'three' ]
notice( $my_array[1] )

$my_array = [ 'one', 'two', 'three', 'four', 'five' ]
notice( $my_array[2] )  # ok
notice( $my_array [2] ) # syntax error

# The first notice would log three, and the second notice would log four.
$my_array = [ 'one', 'two', 'three', 'four', 'five' ]
notice( $my_array[2] )
notice( $my_array[-2] )

$my_array = [ 'one', 'two', 'three', 'four', 'five' ]
$cool_value = $my_array[6] # value is undef

# This manifest would log my_array as a notice, because the expression matches the empty array.
$my_array = []
if $my_array =~ Array[String] {
  notice( 'my_array' )
}
```

### Booleans data type
Booleans are one-bit values, representing true or false.

If a non-boolean value is used where a boolean is required:
- The undef value is converted to boolean false.
- All other values are converted to boolean true.

### Error data type
An Error object contains a non-empty message. It can also contain additional context about why the error occurred.

```python
Error[<MESSAGE>, <KIND>, <DETAILS>, <ISSUE CODE>]
notice($err.msg)
notice($err.kind)
notice($err.issue_code)
notice($err.details)
```

### Hash data type:
```python
{ key1 => 'val1', key2 => 'val2' }
# Equivalent:
{ key1 => 'val1', key2 => 'val2', }

{ 'key1' => ['val1','val2'], 
  'key2' => {  'key3' =>  'val3',  }, 
  'key4' => true,
  'key5' => 12345,
 }

$myhash = { key       => "some value",
            other_key => "some other value" }
notice( $myhash[key] )

$cool_value = $myhash[absent_key] # Value is undef

$main_site = { port        => { http  => 80,
                                https => 443 },
               vhost_name  => 'docs.puppetlabs.com',
               server_name => { mirror0 => 'warbler.example.com',
                                mirror1 => 'egret.example.com' }
             }
notice ( $main_site[port][https] )

```

### Numbers data type:
Numbers are integers and floating point numbers.


### Sensitive data type:
The value is displayed in plain text in the catalog and manifest, but is redacted from logs and reports.

```python
$secret = Sensitive('myPassword')
notice($secret)
```

### String data type:
By default, String matches strings of any length. You can use parameters to restrict which values String matches.

- String: Matches a string of any length.
- String[6]: Matches a string with at least six characters.
- String[6,8]: Matches a string with at least six and at most eight characters.

### Time-related:

#### Timespan datatype:
- Timespan[2]: Matches a Timespan value of 2 seconds.
- Timespan[77.3]: Matches a Timespan value of 1 minute, 17 seconds, and 300 milliseconds (77.3 seconds).
- Timespan['1-00:00:00', '2-00:00:00']: Matches a closed range of Timespan values between 1 and 2 days.

#### timestamp data type:

- Timestamp['2000-01-01T00:00:00.000', default]: Matches an open range of Timestamps from the start of the 21st century to an infinite point in the future.
- Timestamp['2012-10-10']: Matches the exact Timestamp 2012-10-10T00:00:00.0 UTC.
- Timestamp[default, 1433116800]: Matches an open range of Timestamps from an infinite point in the past to 2015-06-01T00:00:00 UTC, here expressed as seconds since the Unix epoch.
- Timestamp['2010-01-01', '2015-12-31T23:59:59.999999999']: Matches a closed range of Timestamps between the start of 2010 and the end of 2015.
