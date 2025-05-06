
# GameIn Platform - Entity Relationship Diagram (ERD)

## 🧩 Entities and Attributes

### 1. User
- `id` (PK)
- `name`
- `email`
- `passwordHash`
- `userType` (enum: Creator, Brand, Community, Admin)
- `profileImage`
- `coverImage`
- `bio`
- `createdAt`

### 2. CreatorProfile
- `id` (PK)
- `userId` (FK → User.id)
- `followersCount`
- `viewersCount`
- `rating`
- `teamId` (FK → Team.id)

### 3. BrandProfile
- `id` (PK)
- `userId` (FK → User.id)
- `companyName`
- `industry`
- `followersCount`
- `rating`
- `verified`

### 4. SponsorshipOffering
- `id` (PK)
- `creatorId` (FK → CreatorProfile.id)
- `type` (e.g., logo_stream, social_post, etc.)
- `basePrice`
- `fee` (5% of base)
- `tax` (15.3%)
- `totalPrice`
- `description`
- `status` (active/inactive)

### 5. Sponsorship
- `id` (PK)
- `brandId` (FK → BrandProfile.id)
- `offeringId` (FK → SponsorshipOffering.id)
- `type` (regular, prize-pool)
- `startDate`
- `endDate`
- `paymentStatus`
- `insights` (JSON)

### 6. Team
- `id` (PK)
- `creatorId` (FK → CreatorProfile.id)
- `name`
- `description`

### 7. TeamMember
- `id` (PK)
- `teamId` (FK → Team.id)
- `memberUserId` (FK → User.id)

### 8. ChatMessage
- `id` (PK)
- `senderId` (FK → User.id)
- `receiverId` (FK → User.id)
- `message`
- `timestamp`

### 9. NewsfeedPost
- `id` (PK)
- `authorId` (FK → User.id)
- `content`
- `type` (text/image/video)
- `createdAt`

### 10. Comment
- `id` (PK)
- `postId` (FK → NewsfeedPost.id)
- `userId` (FK → User.id)
- `text`
- `timestamp`

### 11. Follower
- `id` (PK)
- `followedId` (FK → User.id)
- `followerId` (FK → User.id)
- `followedType` (enum: Creator, Brand)

### 12. AdCampaign
- `id` (PK)
- `createdBy` (FK → User.id)
- `targetType` (audience category)
- `content`
- `cost`
- `impressions`

### 13. Rating
- `id` (PK)
- `userId` (FK → User.id)
- `ratedUserId` (FK → User.id)
- `score`
- `comment`

### 14. SocialLink
- `id` (PK)
- `userId` (FK → User.id)
- `platform` (Instagram, Twitch, etc.)
- `url`
- `followerCount`

### 15. AdminActionLog
- `id` (PK)
- `adminId` (FK → User.id)
- `action`
- `targetEntityId`
- `timestamp`

## 🔗 Key Relationships Summary
- `User` → `CreatorProfile` / `BrandProfile` / `CommunityUser` / `Admin`
- `CreatorProfile` → `SponsorshipOffering`, `Team`
- `BrandProfile` → `Sponsorship`
- `SponsorshipOffering` → `Sponsorship`
- `Team` → `TeamMember` → `User`
- `User` ↔ `ChatMessage`, `NewsfeedPost`, `Comment`, `Follower`, `Rating`, `SocialLink`
- `Admin (User)` → `AdminActionLog`
