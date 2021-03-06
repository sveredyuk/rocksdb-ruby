[![Build Status](https://travis-ci.org/isamu/rocksdb-ruby.svg)](https://travis-ci.org/isamu/rocksdb-ruby)
[![Gem Version](https://badge.fury.io/rb/rocksdb-ruby.svg)](https://badge.fury.io/rb/rocksdb-ruby)

# RocksDB

The rocksdb is a persistent in-process key-value store.

Read more about it here: http://rocksdb.org/

This gem contains Ruby bindings so that you can use it from your Ruby process.

## Installation

First install rocksdb.

Add this line to your application's Gemfile:

```ruby
gem 'rocksdb-ruby'
```

And then execute:

```sh
$ bundle
```

Or install it yourself as:

```sh
$ gem install rocksdb-ruby
```

## Usage

```ruby
require "rocksdb"

# Reads And Writes
key = "test"
value = "1"
rocksdb = RocksDB::DB.new "/tmp/file"
rocksdb.put(key, value)
new_value = rocksdb.get(key)
rocksdb.delete(key)

# Atomic Updates
batch = RocksDB::Batch.new
batch.delete("test:batch1")
batch.put("test:batch2", "b")
rocksdb.write(batch)

# Iteration
iterator = rocksdb.new_iterator

iterator.seek_to_first
while(iterator.valid)
  iterator.value
  iterator.key
  iterator.next
end
iterator.close

# Block
rocksdb.each do |data|
  puts data
end

# Hash access
rocksdb['key'] = data
puts rocksdb['key']


rocksdb.close
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
