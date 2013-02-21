# Cupertino
**CLI for the Apple Dev Center**

Automate administrative tasks that you would normally have to do through the Apple Dev Center websites. Life's too short to manage device identifiers by hand!

> Cupertino is named after [Cupertino, CA](http://en.wikipedia.org/wiki/Cupertino,_California): home to Apple, Inc.'s world headquarters.  
> It's part of a series of world-class command-line utilities for iOS development, which includes, [Shenzhen](https://github.com/mattt/shenzhen) (Building & Distribution), [Houston](https://github.com/mattt/houston) (Push Notifications), [Venice](https://github.com/mattt/venice) (In-App Purchase Receipt Verification), and [Dubai](https://github.com/mattt/dubai) (Passbook pass generation).

## Installation

    $ gem install cupertino

## Usage

### Authentication

    $ ios login


_Credentials are saved in the Keychain. You will not be prompted for your username or password by commands while you are logged in. (Mac only)_

### Devices

    $ ios devices:list

    +------------------------------+---------------------------------------+
    |       Listing 2 devices. You can register 98 additional devices.     |
    +---------------------------+------------------------------------------+
    | Device Name               | Device Identifier                        |
    +---------------------------+------------------------------------------+
    | Johnny Appleseed iPad     | 0123456789012345678901234567890123abcdef |
    | Johnny Appleseed iPhone   | abcdef0123456789012345678901234567890123 |
    +---------------------------+------------------------------------------+

    $ ios devices:add "iPad 1"=abc123
    $ ios devices:add "iPad 2"=def456 "iPad 3"=ghi789 ...

### Provisioning Profiles

    $ ios profiles:list

    +----------------------------------+--------------+---------+
    | Profile                          | App ID       | Status  |
    +----------------------------------+--------------+---------+
    | iOS Team Provisioning Profile: * | ABCDEFG123.* | Valid   |
    +----------------------------------+--------------+---------+

---

    $ ios profiles:manage:devices

_Opens an editor with a list of devices, each of which can be commented / uncommented to turn them off / on for that provisioning profile._

    # Comment / Uncomment Devices to Turn Off / On for Provisioning Profile
    Johnny Appleseed iPad 0123456789012345678901234567890123abcdef
    # Johnny Appleseed iPhone abcdef0123456789012345678901234567890123

### App IDs

    $ ios app_ids:list

    +-----------------------------+------------------------+-------------------+-------------------+
    | Bundle Seed ID              | Description            | Development       | Distribution      |
    +-----------------------------+------------------------+-------------------+-------------------+
    | 123ABCDEFG.com.mattt.bundle | App Bundle Description | Passes            | Passes            |
    |                             |                        | Data Protection   | Data Protection   |
    |                             |                        | iCloud            | iCloud            |
    |                             |                        | In-App Purchase   | In-App Purchase   |
    |                             |                        | Game Center       | Game Center       |
    |                             |                        | Push Notification | Push Notification |
    +-----------------------------+------------------------+-------------------+-------------------+

### Certificates

    $ ios certificates:list

    +------------------+----------------------------------+-----------------+--------+
    | Name             | Provisioning Profiles            | Expiration Date | Status |
    +------------------+----------------------------------+-----------------+--------+
    | Johnny Appleseed | iOS Team Provisioning Profile: * | Dec 23, 2012    | Issued |
    +------------------+----------------------------------+-----------------+--------+

### Pass Type IDs

    $ ios pass_type_ids:add pass.com.example.coupon.myExamplePass --description "My Example Pass Coupon"

    Added pass.com.example.coupon.myExamplePass: My Example Pass Coupon

---

    $ ios pass_type_ids:list

    +------------+--------------------------------------------+--------------+-------------------+
    | Card ID    | Identifier                                 | Description  | Pass Certificates |
    +------------+--------------------------------------------+--------------+-------------------+
    | WWWWWWWWWW | pass.com.example.coupon.myExamplePass      | Coupon       | None              |
    | XXXXXXXXXX | pass.com.example.eventTicket.myExamplePass | Event Ticket | Pass Certificate  |
    | YYYYYYYYYY | pass.com.example.movieTicket.myExamplePass | Movie Ticket | Pass Certificate  |
    | ZZZZZZZZZZ | pass.com.example.test.001                  | Test         | Pass Certificate  |
    +------------+--------------------------------------------+--------------+-------------------+

---

    $ ios pass_type_ids:certificates:add pass.com.example.coupon.myExamplePass --csr /path/to/csr

    Configured pass.com.example.coupon.myExamplePass. Apple is generating the certificate...
    Certificate generated and is ready to be downloaded.

---

    $ ios pass_type_ids:certificates:list pass.com.example.coupon.myExamplePass

    +------------------+------------+-----------------+----------------+
    | Name             | Status     | Expiration Date | Certificate ID |
    +------------------+------------+-----------------+----------------+
    | Pass Certificate | Configured | Nov 21, 2013    | AAAAAAAAAA     |
    +------------------+------------+-----------------+----------------+

---

    $ ios pass_type_ids:certificates:download pass.com.example.coupon.myExamplePass --certificate_id AAAAAAAAAA

    Successfully downloaded: 'AAAAAAAAAA.cer'

## Commands

- `login`
- `logout`

- `devices:add`
- `devices:list`

- `profiles:list`
- `profiles:manage:devices`
- `profiles:download`

- `certificates:list [development|distribution]`
- `certificates:download`

- `app_ids:list`

- `pass_type_ids:list`
- `pass_type_ids:add`
- `pass_type_ids:certificates:list`
- `pass_type_ids:certificates:add`
- `pass_type_ids:certificates:download`

## Contact

Mattt Thompson

- http://github.com/mattt
- http://twitter.com/mattt
- m@mattt.me

## License

Cupertino is available under the MIT license. See the LICENSE file for more info.
