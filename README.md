# README

## Creation

Create a new project:
```
    $rails new rails-stupid-coaching --webpack --skip-active-storage --skip-action-mailbox
    $cd rails-stupid-coaching
```

Start server:
```$rails server```

```$gem install bootstrap -v 4.4.1```

## Ruby version

Rails version: 6.0.2.2
Ruby version: ruby 2.7.1p83 (2020-03-31 revision a0c7c23c9c) [x86_64-darwin18]

## System dependencies

## Configuration

## Database creation

```$rails generate controller questions```

Add an `ask` function in the `QuestionsController` (`app/controllers/questions_controller.rb`):
```
class QuestionsController < ApplicationController
    def ask
    end
end
```

Add to `routes.rb`:
```get '/ask', to: 'questions#ask'```

Check routes:
```$rails routes```

Create a view for `ask` following the Action View convention:
```
$touch app/views/questions/index.html.erb
$touch app/views/questions/ask.html.erb
```
Add the route:
```get '/answer', to: 'questions#answer'```
Add the `answer` function in the `QuestionsController`, so we now have:
```
class QuestionsController < ApplicationController
    def ask
    end

    def answer
    end
end
```
Create a view for `answer`:
```$touch app/views/questions/answer.html.erb```

## Database initialization

```rails db:migrate```

## How to run the test suite

### System Testing

We will use Headless Chrome for System Testing. 

Now replace code within `test/application_system_test_case.rb` by:
```
require "test_helper"

class ApplicationSystemTestCase < ActionDispatch::SystemTestCase
  Capybara.register_driver(:headless_chrome) do |app|
    capabilities = Selenium::WebDriver::Remote::Capabilities.chrome \
      chromeOptions: { args: %w[headless disable-gpu window-size=1280x760] }
    Capybara::Selenium::Driver.new app,
      browser: :chrome, desired_capabilities: capabilities
  end
  driven_by :headless_chrome
end
```

Now create a system test file for questions:
```$rails g system_test questions```

Now open the created file `test/system/questions_test.rb` and type the following:
```
require "application_system_test_case"

class QuestionsTest < ApplicationSystemTestCase
  test "visiting /ask renders the form" do
    visit ask_url
    assert_selector "p", text: "Ask your coach anything"
  end
end
```
Run the test by:
```$rails test:system```


## Services (job queues, cache servers, search engines, etc.)

## Deployment instructions

## ...
