# Requirements: Ghost works

## Introduction

A shared book between one artist and one gallery for the works the artist
has left with the gallery. Each work's whereabouts, condition at every
handover, and payment are on record for both sides. A work nobody can account
for shows as a ghost until someone fixes it. See `.kiro/steering/product.md`.

## Requirement 1: start a book and share it

**User story:** As an artist, I want to start a book and send it to the
gallery, so that we both see the same list.

1. WHEN an artist starts a book THE SYSTEM SHALL ask for the artist's name and the gallery's name and create an empty book.
2. WHEN the book is created THE SYSTEM SHALL show a link to share, with a copy button and a WhatsApp share.
3. WHEN someone opens the link for the first time on a phone THE SYSTEM SHALL ask which side they are (artist or gallery) and their name, once.
4. IF the link is wrong or the book does not exist THEN THE SYSTEM SHALL say so in one line and offer to start a new book.

## Requirement 2: add a work

**User story:** As an artist, I want to add each work I leave, with a photo, so its condition is on record from the start.

1. WHEN a work is added THE SYSTEM SHALL require a title and one photo, and allow year, medium, size, the agreed price in naira and the artist's share in percent.
2. WHEN a photo is chosen THE SYSTEM SHALL shrink it in the browser to about 100 KB before saving.
3. WHEN a work is added THE SYSTEM SHALL record a first handover "with the artist" dated today.

## Requirement 3: hand a work over

**User story:** As either side, I want to record each time a work changes hands, with a photo, so nobody can say it was damaged or missing before.

1. WHEN a handover is recorded THE SYSTEM SHALL require where the work goes (to the gallery, back to the artist, to a buyer), a photo of its condition, and the date.
2. WHEN one side records a handover THE SYSTEM SHALL mark it "waiting" until the other side confirms it with one tap.
3. WHEN the other side confirms THE SYSTEM SHALL keep both names and the time on the handover, and never allow it to be changed afterwards.

## Requirement 4: a sale and the artist's share

**User story:** As an artist, I want to see when a work sells and whether my share has reached me.

1. WHEN the gallery marks a work sold THE SYSTEM SHALL ask the sale price and work out the artist's share from the agreed percent, in whole naira.
2. WHEN the artist's share is paid THE SYSTEM SHALL let the gallery mark it paid with a date and an optional photo of the transfer slip, and let the artist confirm.
3. THE SYSTEM SHALL show, at the top of the book, the total still owed to the artist across all sold works.

## Requirement 5: ghosts

**User story:** As either side, I want any work we cannot account for to stand out, so it gets fixed before it becomes a dispute.

1. THE SYSTEM SHALL show a work as a ghost WHEN its last handover is waiting for more than 7 days, OR it has been with the gallery for more than 90 days with no new condition photo, OR it was sold more than 14 days ago and the artist's share is not paid.
2. THE SYSTEM SHALL say in one short line why each ghost is a ghost and offer the one action that fixes it.
3. WHEN the cause is fixed THE SYSTEM SHALL make the work solid again at once.
4. WHERE the phone asks for reduced motion THE SYSTEM SHALL show a ghost as a dashed outline with no drift or fade.

## Requirement 6: put these works on Galleris

**User story:** As a gallery, I want to show these works online, so collectors can see them.

1. WHEN the gallery presses "Put these works on Galleris" THE SYSTEM SHALL download a spreadsheet with the columns Title, Artist, Year, Medium, Dimensions, Description and Photo file, and a folder of the latest photos named to match the Photo file column.
2. THE SYSTEM SHALL leave out prices, shares, payments and both people's names from that export.
3. THE SYSTEM SHALL then open https://www.gallerismuseum.com/try/ in a new tab with a one-line note on what to do with the files.

## Requirement 7: on any phone

1. THE SYSTEM SHALL open its first screen in under 3 seconds on a slow 3G connection.
2. THE SYSTEM SHALL work with a keyboard alone, with every control at least 44 by 44 pixels and text at WCAG AA contrast.
