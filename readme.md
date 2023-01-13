# PHP 3D Viewer Library

This library is used for simple conversion and viewing of 3D-specific formats in a web application. This library supports these formats currently:

- DWG
- DXF
- STL
- STEP
- STP
- JSX
- X3D

## 1. Prerequirements

For the full function of this library, you need these libraries already installed in your system:

- ImageMagick (https://www.php.net/manual/en/book.imagick.php)
- GD (https://www.php.net/manual/en/ref.image.php)
- Multibyte String (https://www.php.net/manual/en/book.mbstring.php)
- JSON Tokenizer

Do not forget to enable these in your php.ini configuration.

## 2. Installation

The installation of this module depends on the operating system installed on the server. Proceed as follows:

### a) Windows

1. Install the required PHP modules and enable them in your `php.ini` configuration.
2. Copy the `libphp_3d.dll` extension into the `C:\Windows\system32` directory (or any other accessible in your `%PATH%`).
3. Let the webserver reload.

### b) macOS / Mac OS X

1. Install the required PHP extensions into PHP's `ext` directory. Enable them in your `php.ini` file.
2. Copy the `libphp_3d.dylib` extension into the `/usr/local/share/Libraries/etc` directory.
3. a. Load the new system module through `kextload -b libphp_3d.dylib` command (if server tools of OSX are installed) OR
b. Rebuild the PHP's extension directory and restart the PHP service.
4. Restart the webserver.

### c) Linux

1. Install the required PHP extensions in your `php/ext` directory and enable them in your `php.ini` file.
2. Copy the `libphp_3d.so` extension into the system extensions directory (path may be vary by the specific distribution of Linux OS).
3. If not present, add the extension directory into the global `$PATH` variable.
4. Restart the webserver.

## 3. How it works

First, load the 3D Object with the load() function. It returns true if model was loaded successfully, false otherwise.
Then simply call the render() method with the loaded object as the first parameter, and configuration as the second one:

**For example:**
```
$renderer = new Php3DLib();

$configVars = []; // The array with configuration
$model = $renderer->load('../path/to/filename.x3d');

if ($model) {
	$renderer->render($model, $configVars);
}
```

You can now work with the 3D model as easy as with any other JSON string and view it in the browser.


## 4. Configuration

The configuration variables are:

- width: integer or string "`auto`" - The width of the object in pixels
- maxWidth: integer - The maximum width of the object (if zoom enabled)
- height: integer or string "`auto`" - The height of the object in pixels
- maxHeight: integer - The maximum height of the object (if zoom enabled)
- zoom: `true` or `false` - Enables/disables the scaling of object with mouse wheel
- rotate: `true` or `false` - Enables/disables the rotation of object with mouse move
- force: `true` or `false` - Forces the 3D object to be loaded before the whole page starts loading

**Example:**

```
$configVars = [
	'width' => 256,
	'height' => 'auto',
	'zoom' => false,
	'rotate' => true,
];
```