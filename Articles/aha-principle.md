## **AHA Principle**

Are you about to introduce an abstraction in your code? Stop and rethink. Do you really need it?

AHA stands for Avoid Hasty Abstractions 

“*prefer duplication over the wrong abstraction”*  - Sandi Metz 

In our quest for DRY, we often tend to make hasty decisions about introducing an abstraction, only to see later that our abstraction has been filled with conditionals to support all use cases. When there is not enough clarity of changes that are coming in the future, we should wait before creating that cool abstraction, even if that means some duplication of code till the time things become clearer.      

While working on the LLD for Digital Wallet [Github Repo](https://github.com/FOSSKolkata/DigitalWalletApp) I had to hold back from the urge to create an abstraction for offer processors which seemed to have some commonalities. But only when I worked on optional requirements 3 and 4, that I made an informed decision to introduce an abstraction called “TransactionTriggeredOfferProcessor” which contained a template for child classes to follow. I have added some documentation in the repo. Please check it out if you’re interested.    

### Take Aways

- Kent C. Dodds

- DRY is not necessarily a bad thing or always a good thing.
- You cannot tell the future: optimize for current change.
- Duplication is far cheaper than the wrong abstraction, so prefer duplication over the wrong abstraction - Sandi Metz
- Wait for commonalities in duplicate code to scream at you for abstraction.
- If you have “shared code” with many conditionals, resist the urge to add more. Refactor it first.

### Resources

https://kentcdodds.com/blog/aha-programming

https://www.youtube.com/watch?v=wuVy7rwkCfc&list=PLV5CVI1eNcJgNqzNwcs4UKrlJdhfDjshf