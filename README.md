# Base64Code - Base64 Encoder/Decoder Java Library

### INTRODUCTION:

This Java&trade; library implements Base64 encoding and decoding. It was
written because I couldn't find anything like it in the JDK except for an
internal class in com.sun.*, and using classes from this package is
totally unsupported by Sun.

### DIFFERENCES:

Whats differs this library from most others are:
   
1. It supports encoding and decoding of input streams in chunk mode.
2. The size of the internal allocated input buffer can be restricted.
     
When encoding or decoding an string or byte array only the result buffer
gets allocated, the source is used as input buffer.
   
### SPECIFICATION:

This implementation is based on http://en.wikipedia.org/wiki/Base64 and 
RFC 2045 (section 6.8). However, support for the line break mode in 76 
character blocks mentioned in the RFC are not supported, mostly because 
I don't have any use of it.

The library has been verified to produce the same result as other commonly 
used implementations, among them:

* The base64_encode() and base64_decode() functions in PHP.
* The base64 command from GNU coreutils.

### EXAMPLE:

```java
package client;

import java.io.InputStream;
import java.io.OutputStream;
import java.io.IOException;
import se.nowise.codecs.base64.Base64Encoder;
import se.nowise.codecs.base64.Base64Decoder;

public class Main {

    /* 
     * Decode input stream and write decoded result to output stream.
     */
    public static void decode(InputStream in, OutputStream out) {
        Base64Decoder decoder = new Base64Decoder();
        try {
            byte[] result = decoder.decode(in);
            while (result != null) {
                out.write(result);
                result = decoder.decode(in);
            }
        } catch (IOException e) {
            System.err.print(e);
        }
    }

    /* 
     * Encode input stream and write encoded result to output stream.
     */
    public static void encode(InputStream in, OutputStream out) {
        Base64Encoder encoder = new Base64Encoder();
        try {
            byte[] result = encoder.encode(in);
            while (result != null) {
                out.write(result);
                result = encoder.encode(in);
            }
        } catch (IOException e) {
            System.err.print(e);
        }
    }
}
```

### LICENSE:

The Base64Code Java Library is licensed under GPL with the classpath 
exception. This means that you are free to use this library even in 
commercial applications (closed source), see the files COPYING and
COPYING.CLASSPATH for details.

The license gives you permission to (freely) link to and use this library
in unmodified form. If you use (copy) source code from this library to
your application, then the you have to release your work as open source 
as well.

See [GNU Classpath](https://www.gnu.org/software/classpath/license.html) exception document 
for further details, also distibuted in source code (docs/COPYING.CLASSPATH)
