# Alien::Build::Plugin::Download::GitLab ![static](https://github.com/PerlAlien/Alien-Build-Plugin-Download-GitLab/workflows/static/badge.svg) ![linux](https://github.com/PerlAlien/Alien-Build-Plugin-Download-GitLab/workflows/linux/badge.svg)

Alien::Build plugin to download from GitLab

# SYNOPSIS

```perl
use alienfile;

plugin 'Download::GitLab' => (
  gitlab_user    => 'plicease',
  gitlab_project => 'dontpanic',
);
```

# DESCRIPTION

This plugin is designed for downloading assets from a GitLab instance.

# PROPERTIES

## gitlab\_host

The host to fetch from [https://gitlab.com](https://gitlab.com) by default.

## gitlab\_user

The user to fetch from.

## gitlab\_project

The project to fetch from.

## type

The asset type to fetch.  This must be one of `source` or `link`.

## format

The expected format of the asset.  This should be one that
[Alien::Build::Plugin::Extract::Negotiate](https://metacpan.org/pod/Alien::Build::Plugin::Extract::Negotiate) understands.  The
default is `tar.gz`.

## version\_from

Where to compute the version from.  This should be one of
`tag_name` or `name`.  The default is `tag_name`.

## convert\_version

This is an optional code reference, which can be used to modify
the version.  For example, if tags have a `v` prefix you could
remove it like so:

```perl
plugin 'Download::GitLab' => (
  gitlab_user     => 'plicease',
  gitlab_project  => 'dontpanic',
  convert_version => sub {
    my $version = shift;
    $version =~ s/^v//;
    return $version;
  },
);
```

## link\_name

For `link` types, this is a regular expression that filters the
asset filenames.  For example, if there are multiple archive
formats provided, you can get just the gzip'd tarball by setting
this to `qr/\.tar\.gz$/`.

# SEE ALSO

- [Alien](https://metacpan.org/pod/Alien)
- [Alien::Build::Plugin::Download::GitHub](https://metacpan.org/pod/Alien::Build::Plugin::Download::GitHub)
- [alienfile](https://metacpan.org/pod/alienfile)
- [Alien::Build](https://metacpan.org/pod/Alien::Build)

# AUTHOR

Graham Ollis <plicease@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2022 by Graham Ollis.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
