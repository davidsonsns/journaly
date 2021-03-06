# Migration `20200805064655-add-published-at-to-posts`

This migration has been generated by Robin MacPherson at 8/5/2020, 6:46:55 AM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
ALTER TABLE "public"."Post" ADD COLUMN "publishedAt" timestamp(3)   ,
ALTER COLUMN "status" SET DEFAULT 'DRAFT';

ALTER TABLE "public"."User" ALTER COLUMN "userRole" SET DEFAULT 'FREE_USER';
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20200702185801-fix-issues..20200805064655-add-published-at-to-posts
--- datamodel.dml
+++ datamodel.dml
@@ -1,7 +1,7 @@
 datasource db {
   provider = "postgresql"
-  url = "***"
+  url      = env("DATABASE_URL")
 }
 generator prisma_client {
   provider = "prisma-client-js"
@@ -72,28 +72,29 @@
   authorId Int
 }
 model Post {
-  id         Int         @default(autoincrement()) @id
-  title      String
-  body       String
-  bodySrc    String      @default("")
-  excerpt    String
-  status     PostStatus  @default(DRAFT)
-  images     Image[]
-  createdAt  DateTime    @default(now())
-  updatedAt  DateTime    @updatedAt
-  author     User        @relation(fields: [authorId], references: [id])
-  authorId   Int
-  readTime   Int         @default(1)
-  likes      PostLike[]
-  topic      Topic[]     @relation(references: [id])
-  language   Language    @relation(fields: [languageId], references: [id])
-  languageId Int
-  longitude  Float?
-  latitude   Float?
-  threads    Thread[]
-  postTopics PostTopic[]
+  id          Int         @default(autoincrement()) @id
+  title       String
+  body        String
+  bodySrc     String      @default("")
+  excerpt     String
+  status      PostStatus  @default(DRAFT)
+  images      Image[]
+  createdAt   DateTime    @default(now())
+  updatedAt   DateTime    @updatedAt
+  publishedAt DateTime?
+  author      User        @relation(fields: [authorId], references: [id])
+  authorId    Int
+  readTime    Int         @default(1)
+  likes       PostLike[]
+  topic       Topic[]     @relation(references: [id])
+  language    Language    @relation(fields: [languageId], references: [id])
+  languageId  Int
+  longitude   Float?
+  latitude    Float?
+  threads     Thread[]
+  postTopics  PostTopic[]
 }
 model Language {
   id            Int                @default(autoincrement()) @id
```


