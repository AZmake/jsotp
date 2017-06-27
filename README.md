# jsotp

`jsotp` is a node module to generate and verify one-time passwords that were used to implement 2FA and MFA authentication method in web applications and other login-required systems.

The module was implement based on [RFC4226](https://tools.ietf.org/html/rfc4226) (HOTP: An HMAC-Based One-Time Password Algorithm) and [RFC6238](https://tools.ietf.org/html/rfc6238) (TOTP: Time-Based One-Time Password Algorithm)

### Feature

* Generate random base32 encoded string
* Generate a `otpauth url` with the b32 encoded string
* Create a HOTP object with verification
* Verify a HOTP token
* Create a TOTP object with verification
* Verify a TOTP token

### Installation

	npm install jsotp
	
### Module

All features support:

	let jsotp = require('jsotp');
	
Only `Base32` module support:

	let jsotp = require('jsotp/base32');
	
Only `HOTP` module support:

	let jsotp = require('jsotp/hotp');
	
Only `TOTP` module support: 

	let jsotp = require('jsotp/totp');
	
### Usage

#### Time-based OTPs

```javascript
# import
let jsotp = require('jsotp');

# Create TOTP object
let totp = jsotp.TOTP.gen('BASE32_ENCODED_SECRET');
totp.now(); # => 432143

# Verify for current time
totp.verify(432143); # => true

# Verify after 30s
totp.verify(432143); # => false
```

#### Counter-based OTPs

```javascript
# import
let jsotp = require('jsotp');

# Create HOTP object
let hotp = jsotp.HOTP.gen('BASE32_ENCODED_SECRET');
hotp.at(0); # => 432143
hotp.at(1); # => 231434
hotp.at(2132); # => 242432

# Verify with a counter
hotp.verify(242432, 2132); # => true
hotp.verify(242432, 2133); # => false
```

#### Generate random base32 encoded secret

```javascript
# import
let jsotp = require('jsotp');

# Generate
let b32_secret = jsotp.Base32.random_gen();
```

### Api

#### • jsotp.Base32.random_gen()

#### • jsotp.Util.url_gen

#### • jsotp.TOTP.gen()

#### • jsotp.TOTP.now()

#### • jsotp.TOTP.verify()

#### • jsotp.HOTP.gen()

#### • jsotp.HOTP.at()

#### • jsotp.HOTP.verify()

### [中文文档](docs/README_zh.md)

