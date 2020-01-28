# Infographics for newbies

Goal: design simple to understand infographics so newbies can grasp Nyzo specificities, learn the vocabulary and dig more info with the right basis.

The following are scripts suggestions for visuals to be made.  
please discuss and propose improvements.

I listed basic steps, followed by possible extra info.

## A. Nyzo basic working

A1- Nyzo nodes are called verifiers  
A2- Anyone with access to an IPv4 address can run a verifier  
A3- All Verifiers form "the mesh"  
A4- A small portion of verifiers are elected to be part of the cycle.  
A5- in cycle verifiers take turn to forge blocks, and earn rewards from transactions fees

* A2: No PoS, you don't need any nyzo to run a verifier
* A3: the mesh is composed of "the cycle" and "the queue".
* A4: the cycle votes for new verifiers at specific time interval
* A5: no PoW, no halving, no emission. All nyzos exists since the beginning, rewards come from seed account and fees only.

## B. Verifiers life cycle

B1 - A verifier starts, it sends a message to the mesh  
B2 - A 30 days period begins.  
B3 - After 30 days of working, the verifier is eligible to the lottery  
B4 - If/When it wins the lottery, the verifier has to forge a block  
B5 - The verifier is now part of the cycle and will get rewards  
B6 - If a verifier does not forge a block when it's its turn, he drops out of the cycle  
B7 - If a verifier exhibits consistent bad performance metrics, he can be voted out of the cycle  

* B2: The Verifier has to keep the same IPv4 address or the timer resets.  
* B5: once in cycle, the verifier can change IP once per cycle.

> This one can be some kind of timeline

## C. Verifiers and sentinels

C1 - Sentinels are fallbacks for - in queue and in cycle - verifiers.  
C2 - One sentinel can watch over several verifiers (like, 100)  
C3 - A sentinel can produce a join message on behalf of an in-queue verifier elected for the cycle  
C4 - A sentinel can produce a block on behalf of an in-cycle verifier.  
C5 - In practice, a sentinel is required as soon as a verifier enters the lottery time.  

* C1: As such, they are to be hosted on a different machine/host to be effective  
* C2: Sentinel IP has to be whitelosted on the verifiers it protects

# More (infographics or tutos)

## Best practices

## How to enter the cycle

## Make sure a verifier runs

## Fees and rewards

## Circulating supply

## Wallets, Keys and nyzostrings

## Verifier config files

## Understand verifier logs

## Understand sentinel logs

Test
