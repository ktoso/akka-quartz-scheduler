akka-quartz-scheduler
=====================

Quartz Extension and utilities for true scheduling in Akka 2.0+ (right now built against 2.0.x, but will target all versions eventually)

Note that this is named and targeted as akka-quartz-scheduler for a reason: it is *not* a complete port of Quartz. Rather, we utilize the concepts of Quartz' scheduling system to provide a more robust and reliable scheduling component to Akka than the one already available.

As Viktor Klang points out, 'Perhaps the name "Scheduler" was unfortunate, "Deferer" is probably more indicative of what it does.'

The Akka Scheduler is designed to setup events that happen based on durations from the current moment, but also is executed around a HashedWheelTimer – a potential precision loss for jobs.

The goal here is to provide Akka with a scheduling system that is closer to what one would expect for Cron type jobs – setup long-running ActorSystems that can have certain events kick off by Quartz.

Evolving, subject to change, and not curently for public consumption.

Why not just use the Quartz component in Akka's Camel Extension?

    1. To begin with, Akka's Camel extension was *not* available in Akka 2.0.x, only in 2.1+
    2. Camel brings with it a whole architecture change (`Consumers`, `Producers`, etc) and is not exactly "lightweight" to plug in, if all you want is Quartz support 
    3. We wanted to bring the scheduling concept of Quartz into Akka as cleanly as possible with native configuration integration and a lightweight feel

I don't plan on having anything to do with the distributed transaction, persistence, clustering or any other nonsense anytime soon. This is for cron-ey type timing and scheduling.
 
There is the ability in Quartz to pass JobDataMaps around that accrue mutable state across job ticks; we currently do NOT support that to enforce integrity but may expose a deeper actor structure later that gives some ability to work around that, if need arises.

TODO
––––
- find a way to replace quartz.properties with typesafe / akka config and merge over
- ensure the actorsystem shutdown can shut the scheduler in the extension down
- job scheduling
- job execution
- investigate supporting listeners, with actor hookarounds.
- model job as actor in a way that is meaningful
- misfires and recovery model - play nice with supervision, deathwatch, etc [docs page 23 - very close to supervision strategy]
