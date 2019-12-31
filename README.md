# NAME

Mojo::Cache::Role::GetDefault - Default values in get

# STATUS

<div>
    <a href="https://travis-ci.org/srchulo/Mojo-Cache-Role-GetDefault"><img src="https://travis-ci.org/srchulo/Mojo-Cache-Role-GetDefault.svg?branch=master"></a> <a href='https://coveralls.io/github/srchulo/Mojo-Cache-Role-GetDefault?branch=master'><img src='https://coveralls.io/repos/github/srchulo/Mojo-Cache-Role-GetDefault/badge.svg?branch=master' alt='Coverage Status' /></a>
</div>

# SYNOPSIS

    my $cache = Mojo::Cache->new->with_roles('+GetDefault');

    # set 'abc' for $key in the cache if $key does not exist in the cache.
    # 'abc' will also be the return value
    my $value = $cache->get($key, 'abc');

    # sub is called and passed $key if $key does not exist in the cache.
    # Return value is set in cache for $key and returned by get.
    # $key is also available as the first argument
    my $value = $cache->get($key, sub { "default value for key $_" });

    # use get normally without any default value like in Mojo::Cache
    my $value = $cache->get($key);

    # set a default for all gets.
    # this default will be overridden by any default passed to get.
    $cache = $cache->default('abc');
    $cache = $cache->default(sub { ... });

# DESCRIPTION

[Mojo::Cache::Role::GetDefault](https://metacpan.org/pod/Mojo::Cache::Role::GetDefault) allows [Mojo::Cache](https://metacpan.org/pod/Mojo::Cache) to set and return default in ["get"](#get) when a key does not exist.

# ATTRIBUTES

## default

    my $default = $cache->default;
    $cache      = $cache->default('abc');

    # or use a sub that is passed the key as $_ and as the first argument
    $cache = $cache->default(sub { "default value for key $_" });
    $cache = $cache->default(sub { "default value for key $_[0]" });

The default value that is set and returned by ["get"](#get) if a key does not exist in the cache. ["default"](#default) may be a static value or
a subroutine that returns a value. The key is available to the subroutine as `$_` and as the first argument.

You may clear ["default"](#default) with ["clear\_default"](#clear_default).

["default"](#default) will be overridden by any default passed to ["get"](#get).

# METHODS

## get

- get($key, \[$default\])

    # set 'abc' for $key in the cache if $key does not exist in the cache.
    # 'abc' will also be the return value
    my $value = $cache->get($key, 'abc');

    # sub is called and passed $key if $key does not exist in the cache.
    # Return value is set in cache for $key and returned by get.
    # $key is also available as the first argument
    my $value = $cache->get($key, sub { "default value for $_" });

    # use get normally without any default value like in Mojo::Cache
    my $value = $cache->get($key);

["get"](#get) works like ["get" in Mojo::Cache](https://metacpan.org/pod/Mojo::Cache#get), but allows an optional default value to be set and returned if the key does not
exist in the cache. `$default` may be a static value or a subroutine that returns a value. The key is available
to the subroutine as `$_` and as the first argument.

Any `$default` passed to ["get"](#get) will override any default set in ["default"](#default).

Providing no `$default` makes ["get"](#get) behave exactly like ["get" in Mojo::Cache](https://metacpan.org/pod/Mojo::Cache#get).

## clear\_default

    $cache = $cache->clear_default;

Clears any existing default set by ["default"](#default).

## exists

    if ($cache->exists($key)) {
      ...
    }

Returns `true` if a cached value exists for the provided key, `false` otherwise.

["exists"](#exists) is composed from [Mojo::Cache::Role::Exists](https://metacpan.org/pod/Mojo::Cache::Role::Exists). See that module for more information.

# AUTHOR

Adam Hopkins <srchulo@cpan.org>

# COPYRIGHT

Copyright 2019- Adam Hopkins

# LICENSE

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

# SEE ALSO

- [Mojo::Cache](https://metacpan.org/pod/Mojo::Cache)
- [Mojo::Cache::Role::Exists](https://metacpan.org/pod/Mojo::Cache::Role::Exists)
- [Mojo::Base](https://metacpan.org/pod/Mojo::Base)
