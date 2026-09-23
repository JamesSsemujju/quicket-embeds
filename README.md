# Quicket embed examples

Live, working examples of how Quicket ticketing embeds into an organiser's own website, shown by event type.

Every demo on the page is a real widget, not a screenshot. The point of the page is to show an organiser the shape of integration that suits their event, and to make clear where embedding is the wrong answer.

## The patterns

| Event type | Pattern | Why |
|---|---|---|
| Festival and day events | Full inline embed | Tickets are the point of the page |
| Conferences | Register, then buy | Approval gates the purchase, so no per-person codes |
| Sports fixtures | One embed per fixture, tabbed | A season is many events, not one |
| Concerts and club nights | Buy in a pop-up | The page is visual and a widget would break it |
| Theatre and seated | Deep link, not embed | Seat maps need width, an iframe frustrates |
| Marathons and mass entry | Embed plus offline entry | Reaches entrants who will never complete a web checkout |
| Community and free | RSVP embed | Free tickets carry no commission, so a form is wasted effort |
| Private and members | Access code unlock | Hidden ticket types released to a named group |

## Updating it

Everything is in `index.html`. There is no build step, no dependencies and no framework. Open it, edit, commit.

All embeds are driven by one object near the bottom of the file:

```js
const EVENTS = {
  festival: {
    domain: "quicket.co.ug",
    productid: "384462",
    productname: "the-dotb-picnic-2nd-edition"
  },
  conference: null,
  ...
};
```

Set an entry to `null` and a labelled placeholder box appears in its slot. Fill it in and the live widget replaces it. Nothing else in the file needs touching.

Sports fixtures come from a separate list, so you can add as many as you like:

```js
const FIXTURES = [
  { label: "Matchday 1", event: { domain: "quicket.co.ug", productid: "…", productname: "…" } }
];
```

### Where the values come from

In the event dashboard go to **Settings → Integrations → Widget**, set your colours, click **Save Changes**, then copy the iFrame code. It looks like this:

```html
<iframe src="https://www.quicket.co.ug/embed.aspx?productid=384462&productname=the-dotb-picnic-2nd-edition&embed=true&v=2"
  frameborder="0" scrolling="yes" width="100%" height="800"></iframe>
```

Two values out of that URL go into the config: `productid` and `productname`. Use `quicket.co.ug` for Uganda and `quicket.co.ke` for Kenya.

## Notes

Embeds load lazily. Tab panels and the pop-up only fetch their widget when opened, so the page stays fast no matter how many events are added.

This repository is public, which is what GitHub Pages requires on a free account. Do not commit internal pricing, client names, contract terms or anything else that should not be read by a competitor.

## Hosting

Served by GitHub Pages from the `main` branch. Repository **Settings → Pages → Source: Deploy from a branch → main → / (root)**.
