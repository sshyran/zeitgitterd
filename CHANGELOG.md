# Change Log
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/)
and this project adheres to [Semantic Versioning](http://semver.org/).

# 0.9.2+ - [Unreleased]
## Added
- Allow dots in tag names, as long as they are not next to each other
  (i.e., `..` is not allowed)
- Added support for
  [PGP Digital Timestamping Service](http://www.itconsult.co.uk/stamper.htm)
  and improved documentation
- Timestamp our commit id as well with PGP Timestamper
- Configuration now easier: Just look for `EASYCONFIG` in `zeitgitter.conf`
- Added support for (semi-)automatic configuration
- Configuration through environment variables
- Support Docker
- More detailed debug support (see `--debug-level`)
- Minimal support for HTTP `HEAD` requests
- Can use IMAP servers without `IDLE` support (are there still any out there?)

## Fixed
- Correctly handles IMAP `IDLE` responses other than `EXISTS` (especially
  Dovecot's `* OK still here`)
- End line in stamper mails may now also be in last line.

## Changed
- Split into client (git-timestamp) and server (zeitgitterd).
- Calculate a default for `--gnupg-home` to allow `--number-of-gpg-agents` > 1
- Commit log message includes timestamp as well to improve readability for
  `git blame` etc.
- Log message timestamps (including "Found uncommitted data") now say "UTC"
- Renamed all PGP Digital Timestamper related parameters to a common
  `--stamper-` prefix (the old names are still accepted, but deprecated)
- Mail tests now include a (local) configuration file for the site secrets.


# 0.9.2 - 2019-05-10
## Added
- `make apt` installs dependencies on systems supporting `apt`

### Client
- Distributable via PyPI
- Added Python 2.x compatibility; tested with 2.7
- Automatically derive default timestamp branch name from servername
  (first component not named 'igitt') followd by '-timestamps'.
- Better error message when wrong `gnupg` module has been installed

## Fixed
### Client
- Fetch GnuPG key again if missing from keyring. This fixes unexpected
  behavior when running as sudo vs. natively as root.
- Work around a bug in older GnuPG installs (create `pubring.kbx` if it does
  not yet exist before attempting `scan_keys()`).

## Changed
- Higher-level README

### Client
- Is now implemented as a package (`make install` still installs a flat file
  though, for simplicity)


# 0.9.1 - 2019-04-19
## Added
### Client
- `--server` can be set in git config
- Prevent actual duplicate entries created by `git timestamp --branch`
- Documented that `git timestamp --help` does not work and to use `-h`, as
  `--help` is swallowed by `git` and not forwarded to `git-timestamp`.
- Client system tests (require Internet connectivity)

### Server
- Ability to run multiple GnuPG processes (including gpg-agents) in parallel
- Handle missing `--push-repository` (again)

## Fixed
- Made tests compatible with older GnuPG versions

## Changed
### Client
- Made some error messages more consistent
- `--tag` overrides `--branch`. This allows to store a default branch in
  `git config`, yet timestamp a tag when necessary.

# 0.9.0 - 2019-04-04
Initial public release
