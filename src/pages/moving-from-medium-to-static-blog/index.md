---
title: Moving away from Medium
date: '2020-06-16'
spoiler: After a couple of years using Medium as my blog, I decided to move away from Medium and 
    use Gatsby (a static website generator).
tags:
  - Blog
  - Gatsby
  - Github
---

After a couple of years using Medium as my blog, I decided to move away from Medium and 
use [Gatsby](https://www.gatsbyjs.org) (a static website generator).

My main issues with Medium were:
* Limited articles readers can access.
* No code highlight for code-snippets (I always thought this was something that Medium would fix with the time), 
the only alternative was using [Github Gists](https://gist.github.com) but this means that I need to create a Gist 
for every code-snippet that I wanted to show. 
* Internet access was require to write a build my articles.

After checking some alternatives, I ended up considering Gatsby as a really good alternative for the job.
Main advantages of using Gatsby:
* Free hosting using multiples hosting solutions: Github Pages (I'm using this), Netlify and more...
* Static generated (no need for a server to render the pages) during build time.
* I can compose and write articles without internet connection using markdown and view the final 
result in my local environment
* Advance code highlight - I'm using syntax theme based on https://github.com/sdras/night-owl-vscode-theme/ 

Example: 
```php
class DynamoDbMessageRepository implements MessageRepository
{
    /**
     * @var DynamoDbClient
     */
    protected $client;

    /**
     * @var MessageSerializer
     */
    protected MessageSerializer $serializer;

    /**
     * @var string
     */
    protected string $tableName;

    public function __construct(DynamoDbClient $client, MessageSerializer $serializer, string $tableName)
    {
        $this->client = $client;
        $this->serializer = $serializer;
        $this->tableName = $tableName;
    }

    public function retrieveAll(AggregateRootId $id): Generator
    {
        $query = [
            'TableName' => $this->tableName,
            'KeyConditionExpression' => 'aggregateRootId = :v1',
            'ExpressionAttributeValues' => [
                ':v1' => ['S' => $id->toString()],
            ]
        ];

        $result = $this->client->getPaginator('Query', $query);

        return $this->yieldMessagesForResult($result);
    }
}
```
* Great documentation and integration. Gatsby integrates almost with anything and more important it expose 
to developers always the same API in GraphQL independent of what you are connecting 
to (MySQL, Headless CMS, Wordpress, etc...).

Until now, it has been a great experience and I highly recommend you to give it a try. 

---
