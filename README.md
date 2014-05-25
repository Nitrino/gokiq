# Gokiq

Gokiq is a small library to easily enqueue Sidekiq jobs from Go.

## Usage

``` go
// Create a Redis Pool first
pool := redis.NewPool(func() (redis.Conn, error) {
  c, err := redis.Dial("tcp", ":6379")
  if err != nil {
    return nil, err
  }
  return c, err
}, 3)

job := NewJob("HardWorder", "default", []string{"foo", "bar"})

// Enqueue immediately...
job.Enqueue(pool)

// ... or enqueue in the future
now := time.Now()
job.EnqueueAt(now, pool)
```

## Limitations

Currently you can only pass string parameters to your workers.
