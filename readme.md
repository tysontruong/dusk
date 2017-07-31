<p align="center"><img src="http://i.imgur.com/7hqiVYp.png"></p>

<p align="center">
<a href="https://packagist.org/packages/travoltron/dusk-secure"><img src="https://poser.pugx.org/travoltron/dusk-secure/d/total.svg" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/travoltron/dusk-secure"><img src="https://poser.pugx.org/travoltron/dusk-secure/v/stable.svg" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/travoltron/dusk-secure"><img src="https://poser.pugx.org/travoltron/dusk-secure/license.svg" alt="License"></a>
</p>

## What?

Laravel Dusk is an incredibly simple to use browser automation and testing tool. 
However, it was made with testing in mind, and as such, was never really meant for the production environment limelight. 

Not anymore. I've gone ahead and ripped out all the parts that expose routes, or interact with your users. 

## Why?

So we can scrape the web with an amazingly expressive API in a framework we all know and love! All the methods you know and love -- minus the ones on interacting with or acting as users -- are there. See the official docs below for more details. 

## Caveats and gotchas

When using this tool as a scraper, you're typically limited to making dusk tests, and then triggering them via `php artisan dusk`. 

You can automate this process and apply them to a command bus _you can schedule!_

Here's how:

Make your dusk test as you have before. Then, make a new command, making sure to give it a unique signature.

In the handle method, simply new up the class of the test you just created, initialize it and run it:

```
/**
 * Execute the console command.
 *
 * @return mixed
 */
public function handle()
{
    $event = new \Tests\Browser\Test;
    $event->prepare();
    $event->testExample();
}
```

Do whatever you had planned with the data you're scraping *inside the test itself* and you're golden.

When you make a test for dusk, make sure you include `$browser->quit();` to ensure that the browser cleans up after itself. Do this after you've processed the data you've scraped.

## What's next?

I'll make a `2.0` branch in the coming days to keep pace with the official package. It brings headless operation which will really help with some serious scraping. 

If anyone wants to help kick in a PR. 

## Official Documentation

Documentation for Dusk can be found on the [Laravel website](https://laravel.com/docs/master/dusk).

## License

Dusk-Secure is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)
