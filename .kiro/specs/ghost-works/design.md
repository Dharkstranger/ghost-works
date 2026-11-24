# Design: Ghost works

## Overview

One page app. A book is one Firestore document with its works; each work
holds its handovers. The pure modules (`book`, `ghost`, `share`, `export`)
hold every rule and are tested alone; the screens only show them.

## Data

```ts
type Side = 'artist' | 'gallery';
type Book = { id: string; artistName: string; galleryName: string; createdAt: string; works: Work[] };
type Work = {
  id: string; title: string; year?: string; medium?: string; size?: string;
  priceNaira?: number; sharePercent?: number;          // agreed when it is left
  handovers: Handover[];                                // oldest first, never edited
  sale?: { priceNaira: number; soldAt: string; paid?: { at: string; slipPhoto?: string; confirmedBy?: Side } };
};
type Handover = {
  id: string; to: 'artist' | 'gallery' | 'buyer'; at: string; photo: string;  // photo: about 100 KB, base64
  by: Side; byName: string; confirmed?: { by: Side; name: string; at: string };
};
```

A Firestore document holds up to 1 MB, so a book keeps the newest photo
per handover at about 100 KB and starts a second document past 8 works'
worth of photos (`store.ts` hides this from the screens).

## The ghost rules (`ghost.ts`)

`whyGhost(work, now): Reason | null`, where Reason is one of
`waiting` (last handover unconfirmed for over 7 days), `unseen` (with the
gallery over 90 days with no new photo), `unpaid` (sold over 14 days ago,
share not paid). The order above is the order shown when more than one
applies. Pure: the same work and time always give the same answer.

## The share (`share.ts`)

`shareOf(price, percent)` rounds down to whole naira; `galleryPart = price -
share`; the two always add up to the price. `owed(book)` sums the shares of
sold works not yet paid.

## Screens

1. **Start**: two names, one button.
2. **The book**: the total still owed at the top; then every work as a card.
   A ghost card is translucent, drifts slowly, and shows its one line and its
   one button ("Confirm handover", "Add a photo", "Mark paid").
3. **A work**: its handovers as a strip of photos with dates and names.
4. **Hand over** and **Sold** sheets: one question each.
5. **Put these works on Galleris**: from the book's menu.

Look: night colours (ink, bone, one candle orange for actions), solid works
in full colour, ghosts in pale mist. The spooky look only ever marks what is
unaccounted for.

## Errors

No connection: changes wait on the phone and go when it is back, with a small
"Not sent yet" line. A photo too large: shrunk again, never refused.

## Testing

Unit tests for every pure module. Property tests (fast-check): for any price
and percent, share + gallery part = price and share >= 0; a work with a
confirmed handover in the last 7 days, a photo in the last 90 days, and no
unpaid sale is never a ghost; fixing the cause always clears that reason.
