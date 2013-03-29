# AWSCloudSearch

## Description

This gem is an implementation of the Amazon Web Service CloudSearch API (http://aws.amazon.com/cloudsearch/).

The AWS CloudSearch service is comprised of three API end points: search, document batching, and configuration. This gem
currently supports only the search and document batching APIs

## Roadmap

Spoke developed this library in a short period of time in order to migrate from IndexTank to AWS CloudSearch.
As such, there are a few features that are missing that we would like to build over time.

+ Implementation of the configuration API
+ Query builder
+ Faceting helpers
+ Spec tests that stub the AWS CloudSearch service
+ Sample usage in this README

## Installation

Add this line to your application's Gemfile:

    gem 'aws_cloud_search'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install aws_cloud_search

## Usage

*Note*: work in progress


1. Initialize the library

```ruby
ds = AWSCloudSearch::CloudSearch.new(ENV['CLOUDSEARCH_DOMAIN'])
```

2. Create some documents. `Document#new` takes an optional parameter `auto_version` which you set to true to automatically set the version, the default value is false.

```ruby
doc1 = AWSCloudSearch::Document.new(true)
doc1.id = '12345677890abcef'
doc1.lang = 'en'
doc1.add_field('name', 'Jane Williams')
doc1.add_field('type', 'person')

doc2 = AWSCloudSearch::Document.new(true)
doc2.id = Array.new( 8 ) { rand(256) }.pack('C*').unpack('H*').first
doc2.lang = 'en'
doc2.add_field :name, 'Bob Dobalina'
doc2.add_field :type, 'person'
```

3. Create a new document batch

```ruby
batch = AWSCloudSearch::DocumentBatch.new    
batch.add_document doc1
batch.add_document doc2
```

4. Send the document batch

```ruby
ds.documents_batch(batch)
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## Version History

0.0.2 Added support for faceting
