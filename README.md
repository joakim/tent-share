**This is a suggestion for a new post type, it does not yet exist. WIP. See [Thoughts](#thoughts) for more.**

See also my suggestion for the related [Link](https://github.com/joakim/tent-link) post type.

# Share

Something that is shared.

A very basic post type consisting of only a short text (optional), and referencing the thing that is shared. By applying the basic abilities of Tent's [post](https://tent.io/docs/posts) metadata (references, permissions, mentions), this becomes a very versatile yet very simple way to share basically anything. Well, anything you can reference in Tent.

The thing to be shared is specified by the `refs` property. Recipients and privacy of a share is controlled by the `mentions` and `permissions` properties. An optional short text may be added to the `message` content field.

#### Schema

| Property | Required | Type | Description |
| -------- | -------- | ---- | ----------- |
| `message` | Optional | String | A short text about this share from the owner of the post. |

#### Example

```json
{
  "content": {
    "message": "An interesting article on link sharing, and how most of it happens outside of the traditional social networks.",
  },
  "refs": [
    //"Reference to a link post (the link that is shared)"
  ],
  "mentions": [
    //"Recipients of the share"
  ],
  "permissions": {
    "groups": [
      //"Groups permitted to see the share"
    ],
    "entities": [
      //"Entities permitted to see the share"
    ]
  }
}
```

## Thoughts

(This turned into more of a blog post/rant than I had planned..!)

### Some background

Sharing a link is older than the web itself, and did not arrive with social networking. The Atlantic wrote an interesting article called [Dark Social: We Have the Whole History of the Web Wrong](http://www.theatlantic.com/technology/archive/2012/10/dark-social-we-have-the-whole-history-of-the-web-wrong/263523/), explaining how most sharing happens outside of social networks.

This also means that still, in 2013, we mostly use copy + paste to share something we find interesting.

To illustrate, this is how we often share links today:

1. Copy the link from the address bar
2. Open Facebook/Twitter/Tumblr/email/chat
3. Paste the link
4. Type in the recipients and a little text
5. And finally, click Send

There has to be an easier way. Sure, there's myriad of social sharing buttons. It's all kinda messy, you have to decide which walled garden to share to, and they're all eating your soul (well, your privacy at least). And as The Atlantic has shown, these walled gardens only account for about 30% of all sharing (for media sites at least).

Tent provides a great opportunity to revolutionize sharing. The protocol is more than flexible and powerful enough for any sharing needs, your Tent server keeps all your contacts (up-to-date), it's near-realtime, and you have full control over your privacy.

I also see possibilities beyond simply sharing links, which is why a URL is not included as a field in this post type. To share a link, a `share` post would reference a [link](https://github.com/joakim/tent-link) post. See [Share _anything_, you say?](#share-anything-you-say) for more on this.

#### Why not simply use `status`?

Status posts are designed for conversations, having been modeled after Twitter. While there's a lot of link sharing happening on Twitter (and Cupcake), sharing may also happen outside of conversations. In fact around 70% happens outside of social, as The Atlantic has shown.

Having a separate post type for sharing opens up for a whole range of new apps and use cases. It also gives it a semantic meaning. Sharing some _thing_ is an action that is very different from sharing some _thoughts_ or participating in a discussion.

That said, the relationship to `status` seems a bit tricky. One could `share` a `status` (which would be different from a repost), and a `status` post could reference a `share`. Not yet sure what this could mean, or how to avoid any problems there.

#### How would apps use this?

Sharing over Tent supersedes sharing over email and social networks.

[Potluck](https://www.potluck.it/) is one example of an app dedicated to link sharing.

Twitter-like apps (such as Cupcake) could also add support for `share`, alongside `status`. That would result in something closer to Facebook's news feed. A lot of what you see on Facebook is images and videos with a short text. In the context of this suggestion, that would be a `share` post with a message, referencing a `link` post.

For an app to share a link, it would first create a `link` post, then create a `share` post referencing it. The interface would of course simplify this for the user. One would either copy + paste as today, or better, have a universal "Share on Tent" button to embed on websites, or even better, a browser plugin that lets you share whatever you're viewing with the click of a button. To the whole world, or to someone specific. (I'm working on this…)

A `share` post may reference posts of any type. But people are used to only share links, and I expect that's what this post type would be used for to begin with. So apps should as a minimum be able to render a link. It could be as easy as outputting the URL as a link, or as awesome as rendering an embed or a preview of the link's destination using something like [IFramely](http://iframely.com/). Easily beats Facebook's limited previews and Twitter's whitelisted cards.

#### Share _anything_, you say?

A link can point to anywhere on the web. But let's think bigger than that. A `share` may reference any Tent post type, so it would only be limited by the post types that are and what they can do. Photos, songs, files. You could even think of the [Internet of Things](https://www.youtube.com/watch?feature=player_embedded&v=yDYCf4ONh5M). You could share a book you just read (sharing its UUID instead of a link to Amazon), a physical location (referencing a `location` post instead of a Google Maps link), or the episode of a TV show you're watching (referencing its UUID from some standardized TV episode database), or a specific airline flight. So yes, _anything_.

This is not the same as creating e.g. a `location` post or a specialized app creating an `episode` post. You could (and possibly would) of course do that as well. But those posts would only be read by users and apps who have subscribed to those post types. `share` is what you'd use when you want to push something to someone else (or the whole world).

Because a `share` has the ability to reference any Tent post, supporting apps would have to have knowledge of the referenced post's type to be able to correctly render it. Machine-readable post schemas should make this a bit easier. It could also open up nicely for new "embed services" similar to IFramely and Embedly.
