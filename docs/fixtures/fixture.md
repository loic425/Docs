# 7.2 - How to configure your fixture options

Now you have to create a fixture service. This defines options you can use on [fixtures bundle configurations yaml files](https://github.com/Monofony/Monofony/blob/0.x/src/Monofony/Pack/CorePack/.recipe/config/sylius/fixtures.yaml).

```php
<?php

declare(strict_types=1);

namespace App\Fixture;

use Monofony\Plugin\FixturesPlugin\Fixture\AbstractResourceFixture;
use Symfony\Component\Config\Definition\Builder\ArrayNodeDefinition;

class ArticleFixture extends AbstractResourceFixture
{
    public function __construct(ObjectManager $objectManager, ArticleExampleFactory $articleExampleFactory)
    {
        parent::__construct($objectManager, $articleExampleFactory);
    }

    /**
     * {@inheritdoc}
     */
    public function getName(): string
    {
        return 'article';
    }

    /**
     * {@inheritdoc}
     */
    protected function configureResourceNode(ArrayNodeDefinition $resourceNode)
    {
        $resourceNode
            ->children()
                ->scalarNode('title')->cannotBeEmpty()->end()
        ;
    }
}
```

In this file we have only one custom option which is the article title.

Thanks to autowiring system, you can already use it.

```bash
$ bin/console debug:container App\Fixture\ArticleFixture
```
