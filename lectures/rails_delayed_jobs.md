## Rails delayed jobs

Delayed jobs are used for asynchronously executing longer tasks in the background. 

In this lecture you will learn when and how to use the delayed jobs for background processing.

### Use case 

- sending massive newsletters
- image resizing
- http downloads/uploads (you can prevent page lock until download is finished )
- batch imports
- spam checks

... and so on.

---

### Installation

Add following to your Gemfile:
```rb
gem 'delayed_job_active_record'
```

Run ```bundle install``` to install the backend and delayed_job gems.

The Active Record backend requires a jobs table. You can create that table by running the following command:
```rb
rails generate delayed_job:active_record
rake db:migrate
```

After that you have to specify the queue adapter in the config/application.rb
```rb
config.active_job.queue_adapter = :delayed_job
```
... and we can create our jobs now!

Here's an example of a heavy(long) process which is beeing simulated by using the default Ruby method ```sleep```:
```rb
Class MyJob
  def perform
    sleep(10)
    puts 'The process is finished using delayed job!'
  end
end
```

### Usefull links:
-----------------------------------

- https://www.youtube.com/watch?v=9twx2YFPzZo (Screencast of the previous rubylab lecture)
- https://github.com/collectiveidea/delayed_job (Link to the gem's github with thew documentation)
- https://guides.rubyonrails.org/active_job_basics.html

