# How to compress project code in Ruby on Rails.

Compressing your code is one of the best practices that you can do, because it allows the server to run your project faster and more efficiently. So, the goal of this tutorial is to help you to do that.

__First of all, if you don't know how to create a project or install Rails on your machine, check the link bellow:__

[https://gorails.com/setup/ubuntu/16.04](https://gorails.com/setup/ubuntu/16.04)

I´m using Ubuntu to develop because it's easier to create and manage the project. Feel free to use other OS of your choice.

## Required gems:
- [htmlcompressor](https://rubygems.org/gems/htmlcompressor)

Well, after the project is created, you'll need to add the gem 'htmlcompressor' on Gemfile:
```
gem 'htmlcompressor', '~> 0.3.0'
```

And then, execute the command on terminal:
```
gem install htmlcompressor
```

With this, the project will have the gem activated.
After this you can create a Library element, which I name __MyCompressor__

__lib/MyCompressor.rb__
```
class MyCompressor

end
```

Inside the class we will create a function to compress our code.

### _Why do we have to create this if we already installed a gem?_
Because the gem works to compress html, but to compress css and js, we need a function.
On this link [https://github.com/paolochiodi/htmlcompressor](https://github.com/paolochiodi/htmlcompressor) you can read more about it.

I created the function compress
```
def compress(source)
	return source.gsub("\n", ' ').squeeze(' ')
end
```
__gsub__ will remove all breaklines on code, insert spaces.

__squeeze__ will remove all duplicate spaces between the data.

And finally we will open the __config/environments/development.rb__ and insert this code:

```
require 'MyCompressor'
```

To call the Library that you created to compress all css and js on your page.
And...

```  
config.middleware.use HtmlCompressor::Rack, options = {
	:compress_css => true,
	:css_compressor => MyCompressor.new,
	:compress_javascript => true,
	:javascript_compressor => MyCompressor.new
}
```

Define with the gem that we installed, we will be allowed to compress css an js with our code.
Finally your code is compressed. 

If you have a better way to do this, feel free to share to me and other engineers.
