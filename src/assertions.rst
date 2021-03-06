

.. _appendixes.assertions:

==========
Assertions
==========

This appendix lists the various assertion methods that are available.

.. _appendixes.assertions.static-vs-non-static-usage-of-assertion-methods:

Static vs. Non-Static Usage of Assertion Methods
################################################

PHPUnit's assertions are implemented in PHPUnit\\Framework\\Assert.
PHPUnit\\Framework\\TestCase inherits from PHPUnit\\Framework\\Assert.

The assertion methods are declared static and can be invoked
from any context using PHPUnit\\Framework\\Assert::assertTrue(),
for instance, or using $this->assertTrue() or self::assertTrue(),
for instance, in a class that extends PHPUnit\\Framework\\TestCase.

In fact, you can even use global function wrappers such as assertTrue() in
any context (including classes that extend PHPUnit\\Framework\\TestCase)
when you (manually) include the :file:`src/Framework/Assert/Functions.php`
sourcecode file that comes with PHPUnit.

A common question, especially from developers new to PHPUnit, is whether
using $this->assertTrue() or self::assertTrue(),
for instance, is "the right way" to invoke an assertion. The short answer
is: there is no right way. And there is no wrong way, either. It is a
matter of personal preference.

For most people it just "feels right" to use $this->assertTrue()
because the test method is invoked on a test object. The fact that the
assertion methods are declared static allows for (re)using
them outside the scope of a test object. Lastly, the global function
wrappers allow developers to type less characters (assertTrue() instead
of $this->assertTrue() or self::assertTrue()).

.. _appendixes.assertions.assertArrayHasKey:

assertArrayHasKey()
###################

``assertArrayHasKey(mixed $key, array $array[, string $message = ''])``

Reports an error identified by ``$message`` if ``$array`` does not have the ``$key``.

``assertArrayNotHasKey()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertArrayHasKey()
    :name: appendixes.assertions.assertArrayHasKey.example

    <?php
    use PHPUnit\Framework\TestCase;

    class ArrayHasKeyTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertArrayHasKey('foo', ['bar' => 'baz']);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit ArrayHasKeyTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) ArrayHasKeyTest::testFailure
    Failed asserting that an array has the key 'foo'.

    /home/sb/ArrayHasKeyTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertClassHasAttribute:

assertClassHasAttribute()
#########################

``assertClassHasAttribute(string $attributeName, string $className[, string $message = ''])``

Reports an error identified by ``$message`` if ``$className::attributeName`` does not exist.

``assertClassNotHasAttribute()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertClassHasAttribute()
    :name: appendixes.assertions.assertClassHasAttribute.example

    <?php
    use PHPUnit\Framework\TestCase;

    class ClassHasAttributeTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertClassHasAttribute('foo', stdClass::class);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit ClassHasAttributeTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 4.75Mb

    There was 1 failure:

    1) ClassHasAttributeTest::testFailure
    Failed asserting that class "stdClass" has attribute "foo".

    /home/sb/ClassHasAttributeTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertArraySubset:

assertArraySubset()
###################

``assertArraySubset(array $subset, array $array[, bool $strict = false, string $message = ''])``

Reports an error identified by ``$message`` if ``$array`` does not contains the ``$subset``.

``$strict`` is a flag used to compare the identity of objects within arrays.

.. code-block:: php
    :caption: Usage of assertArraySubset()
    :name: appendixes.assertions.assertArraySubset.example

    <?php
    use PHPUnit\Framework\TestCase;

    class ArraySubsetTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertArraySubset(['config' => ['key-a', 'key-b']], ['config' => ['key-a']]);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit ArraySubsetTest
    PHPUnit 7.0.0 by Sebastian Bergmann.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) Epilog\EpilogTest::testNoFollowOption
    Failed asserting that an array has the subset Array &0 (
        'config' => Array &1 (
            0 => 'key-a'
            1 => 'key-b'
        )
    ).

    /home/sb/ArraySubsetTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertClassHasStaticAttribute:

assertClassHasStaticAttribute()
###############################

``assertClassHasStaticAttribute(string $attributeName, string $className[, string $message = ''])``

Reports an error identified by ``$message`` if ``$className::attributeName`` does not exist.

``assertClassNotHasStaticAttribute()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertClassHasStaticAttribute()
    :name: appendixes.assertions.assertClassHasStaticAttribute.example

    <?php
    use PHPUnit\Framework\TestCase;

    class ClassHasStaticAttributeTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertClassHasStaticAttribute('foo', stdClass::class);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit ClassHasStaticAttributeTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 4.75Mb

    There was 1 failure:

    1) ClassHasStaticAttributeTest::testFailure
    Failed asserting that class "stdClass" has static attribute "foo".

    /home/sb/ClassHasStaticAttributeTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertContains:

assertContains()
################

``assertContains(mixed $needle, Iterator|array $haystack[, string $message = ''])``

Reports an error identified by ``$message`` if ``$needle`` is not an element of ``$haystack``.

``assertNotContains()`` is the inverse of this assertion and takes the same arguments.

``assertAttributeContains()`` and ``assertAttributeNotContains()`` are convenience wrappers that use a ``public``, ``protected``, or ``private`` attribute of a class or object as the haystack.

.. code-block:: php
    :caption: Usage of assertContains()
    :name: appendixes.assertions.assertContains.example

    <?php
    use PHPUnit\Framework\TestCase;

    class ContainsTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertContains(4, [1, 2, 3]);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit ContainsTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) ContainsTest::testFailure
    Failed asserting that an array contains 4.

    /home/sb/ContainsTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

``assertContains(string $needle, string $haystack[, string $message = '', boolean $ignoreCase = false])``

Reports an error identified by ``$message`` if ``$needle`` is not a substring of ``$haystack``.

If ``$ignoreCase`` is ``true``, the test will be case insensitive.

.. code-block:: php
    :caption: Usage of assertContains()
    :name: appendixes.assertions.assertContains.example2

    <?php
    use PHPUnit\Framework\TestCase;

    class ContainsTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertContains('baz', 'foobar');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit ContainsTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) ContainsTest::testFailure
    Failed asserting that 'foobar' contains "baz".

    /home/sb/ContainsTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. code-block:: php
    :caption: Usage of assertContains() with $ignoreCase
    :name: appendixes.assertions.assertContains.example3

    <?php
    use PHPUnit\Framework\TestCase;

    class ContainsTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertContains('foo', 'FooBar');
        }

        public function testOK()
        {
            $this->assertContains('foo', 'FooBar', '', true);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit ContainsTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F.

    Time: 0 seconds, Memory: 2.75Mb

    There was 1 failure:

    1) ContainsTest::testFailure
    Failed asserting that 'FooBar' contains "foo".

    /home/sb/ContainsTest.php:6

    FAILURES!
    Tests: 2, Assertions: 2, Failures: 1.

.. _appendixes.assertions.assertContainsOnly:

assertContainsOnly()
####################

``assertContainsOnly(string $type, Iterator|array $haystack[, boolean $isNativeType = null, string $message = ''])``

Reports an error identified by ``$message`` if ``$haystack`` does not contain only variables of type ``$type``.

``$isNativeType`` is a flag used to indicate whether ``$type`` is a native PHP type or not.

``assertNotContainsOnly()`` is the inverse of this assertion and takes the same arguments.

``assertAttributeContainsOnly()`` and ``assertAttributeNotContainsOnly()`` are convenience wrappers that use a ``public``, ``protected``, or ``private`` attribute of a class or object as the haystack.

.. code-block:: php
    :caption: Usage of assertContainsOnly()
    :name: appendixes.assertions.assertContainsOnly.example

    <?php
    use PHPUnit\Framework\TestCase;

    class ContainsOnlyTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertContainsOnly('string', ['1', '2', 3]);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit ContainsOnlyTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) ContainsOnlyTest::testFailure
    Failed asserting that Array (
        0 => '1'
        1 => '2'
        2 => 3
    ) contains only values of type "string".

    /home/sb/ContainsOnlyTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertContainsOnlyInstancesOf:

assertContainsOnlyInstancesOf()
###############################

``assertContainsOnlyInstancesOf(string $classname, Traversable|array $haystack[, string $message = ''])``

Reports an error identified by ``$message`` if ``$haystack`` does not contain only instances of class ``$classname``.

.. code-block:: php
    :caption: Usage of assertContainsOnlyInstancesOf()
    :name: appendixes.assertions.assertContainsOnlyInstancesOf.example

    <?php
    use PHPUnit\Framework\TestCase;

    class ContainsOnlyInstancesOfTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertContainsOnlyInstancesOf(
                Foo::class,
                [new Foo, new Bar, new Foo]
            );
        }
    }
    ?>

.. code-block:: bash

    $ phpunit ContainsOnlyInstancesOfTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) ContainsOnlyInstancesOfTest::testFailure
    Failed asserting that Array ([0]=> Bar Object(...)) is an instance of class "Foo".

    /home/sb/ContainsOnlyInstancesOfTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertCount:

assertCount()
#############

``assertCount($expectedCount, $haystack[, string $message = ''])``

Reports an error identified by ``$message`` if the number of elements in ``$haystack`` is not ``$expectedCount``.

``assertNotCount()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertCount()
    :name: appendixes.assertions.assertCount.example

    <?php
    use PHPUnit\Framework\TestCase;

    class CountTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertCount(0, ['foo']);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit CountTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 4.75Mb

    There was 1 failure:

    1) CountTest::testFailure
    Failed asserting that actual size 1 matches expected size 0.

    /home/sb/CountTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertDirectoryExists:

assertDirectoryExists()
#######################

``assertDirectoryExists(string $directory[, string $message = ''])``

Reports an error identified by ``$message`` if the directory specified by ``$directory`` does not exist.

``assertDirectoryNotExists()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertDirectoryExists()
    :name: appendixes.assertions.assertDirectoryExists.example

    <?php
    use PHPUnit\Framework\TestCase;

    class DirectoryExistsTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertDirectoryExists('/path/to/directory');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit DirectoryExistsTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 4.75Mb

    There was 1 failure:

    1) DirectoryExistsTest::testFailure
    Failed asserting that directory "/path/to/directory" exists.

    /home/sb/DirectoryExistsTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertDirectoryIsReadable:

assertDirectoryIsReadable()
###########################

``assertDirectoryIsReadable(string $directory[, string $message = ''])``

Reports an error identified by ``$message`` if the directory specified by ``$directory`` is not a directory or is not readable.

``assertDirectoryNotIsReadable()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertDirectoryIsReadable()
    :name: appendixes.assertions.assertDirectoryIsReadable.example

    <?php
    use PHPUnit\Framework\TestCase;

    class DirectoryIsReadableTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertDirectoryIsReadable('/path/to/directory');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit DirectoryIsReadableTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 4.75Mb

    There was 1 failure:

    1) DirectoryIsReadableTest::testFailure
    Failed asserting that "/path/to/directory" is readable.

    /home/sb/DirectoryIsReadableTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertDirectoryIsWritable:

assertDirectoryIsWritable()
###########################

``assertDirectoryIsWritable(string $directory[, string $message = ''])``

Reports an error identified by ``$message`` if the directory specified by ``$directory`` is not a directory or is not writable.

``assertDirectoryNotIsWritable()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertDirectoryIsWritable()
    :name: appendixes.assertions.assertDirectoryIsWritable.example

    <?php
    use PHPUnit\Framework\TestCase;

    class DirectoryIsWritableTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertDirectoryIsWritable('/path/to/directory');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit DirectoryIsWritableTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 4.75Mb

    There was 1 failure:

    1) DirectoryIsWritableTest::testFailure
    Failed asserting that "/path/to/directory" is writable.

    /home/sb/DirectoryIsWritableTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertEmpty:

assertEmpty()
#############

``assertEmpty(mixed $actual[, string $message = ''])``

Reports an error identified by ``$message`` if ``$actual`` is not empty.

``assertNotEmpty()`` is the inverse of this assertion and takes the same arguments.

``assertAttributeEmpty()`` and ``assertAttributeNotEmpty()`` are convenience wrappers that can be applied to a ``public``, ``protected``, or ``private`` attribute of a class or object.

.. code-block:: php
    :caption: Usage of assertEmpty()
    :name: appendixes.assertions.assertEmpty.example

    <?php
    use PHPUnit\Framework\TestCase;

    class EmptyTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertEmpty(['foo']);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit EmptyTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 4.75Mb

    There was 1 failure:

    1) EmptyTest::testFailure
    Failed asserting that an array is empty.

    /home/sb/EmptyTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertEqualXMLStructure:

assertEqualXMLStructure()
#########################

``assertEqualXMLStructure(DOMElement $expectedElement, DOMElement $actualElement[, boolean $checkAttributes = false, string $message = ''])``

Reports an error identified by ``$message`` if the XML Structure of the DOMElement in ``$actualElement`` is not equal to the XML structure of the DOMElement in ``$expectedElement``.

.. code-block:: php
    :caption: Usage of assertEqualXMLStructure()
    :name: appendixes.assertions.assertEqualXMLStructure.example

    <?php
    use PHPUnit\Framework\TestCase;

    class EqualXMLStructureTest extends TestCase
    {
        public function testFailureWithDifferentNodeNames()
        {
            $expected = new DOMElement('foo');
            $actual = new DOMElement('bar');

            $this->assertEqualXMLStructure($expected, $actual);
        }

        public function testFailureWithDifferentNodeAttributes()
        {
            $expected = new DOMDocument;
            $expected->loadXML('<foo bar="true" />');

            $actual = new DOMDocument;
            $actual->loadXML('<foo/>');

            $this->assertEqualXMLStructure(
              $expected->firstChild, $actual->firstChild, true
            );
        }

        public function testFailureWithDifferentChildrenCount()
        {
            $expected = new DOMDocument;
            $expected->loadXML('<foo><bar/><bar/><bar/></foo>');

            $actual = new DOMDocument;
            $actual->loadXML('<foo><bar/></foo>');

            $this->assertEqualXMLStructure(
              $expected->firstChild, $actual->firstChild
            );
        }

        public function testFailureWithDifferentChildren()
        {
            $expected = new DOMDocument;
            $expected->loadXML('<foo><bar/><bar/><bar/></foo>');

            $actual = new DOMDocument;
            $actual->loadXML('<foo><baz/><baz/><baz/></foo>');

            $this->assertEqualXMLStructure(
              $expected->firstChild, $actual->firstChild
            );
        }
    }
    ?>

.. code-block:: bash

    $ phpunit EqualXMLStructureTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    FFFF

    Time: 0 seconds, Memory: 5.75Mb

    There were 4 failures:

    1) EqualXMLStructureTest::testFailureWithDifferentNodeNames
    Failed asserting that two strings are equal.
    --- Expected
    +++ Actual
    @@ @@
    -'foo'
    +'bar'

    /home/sb/EqualXMLStructureTest.php:9

    2) EqualXMLStructureTest::testFailureWithDifferentNodeAttributes
    Number of attributes on node "foo" does not match
    Failed asserting that 0 matches expected 1.

    /home/sb/EqualXMLStructureTest.php:22

    3) EqualXMLStructureTest::testFailureWithDifferentChildrenCount
    Number of child nodes of "foo" differs
    Failed asserting that 1 matches expected 3.

    /home/sb/EqualXMLStructureTest.php:35

    4) EqualXMLStructureTest::testFailureWithDifferentChildren
    Failed asserting that two strings are equal.
    --- Expected
    +++ Actual
    @@ @@
    -'bar'
    +'baz'

    /home/sb/EqualXMLStructureTest.php:48

    FAILURES!
    Tests: 4, Assertions: 8, Failures: 4.

.. _appendixes.assertions.assertEquals:

assertEquals()
##############

``assertEquals(mixed $expected, mixed $actual[, string $message = ''])``

Reports an error identified by ``$message`` if the two variables ``$expected`` and ``$actual`` are not equal.

``assertNotEquals()`` is the inverse of this assertion and takes the same arguments.

``assertAttributeEquals()`` and ``assertAttributeNotEquals()`` are convenience wrappers that use a ``public``, ``protected``, or ``private`` attribute of a class or object as the actual value.

.. code-block:: php
    :caption: Usage of assertEquals()
    :name: appendixes.assertions.assertEquals.example

    <?php
    use PHPUnit\Framework\TestCase;

    class EqualsTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertEquals(1, 0);
        }

        public function testFailure2()
        {
            $this->assertEquals('bar', 'baz');
        }

        public function testFailure3()
        {
            $this->assertEquals("foo\nbar\nbaz\n", "foo\nbah\nbaz\n");
        }
    }
    ?>

.. code-block:: bash

    $ phpunit EqualsTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    FFF

    Time: 0 seconds, Memory: 5.25Mb

    There were 3 failures:

    1) EqualsTest::testFailure
    Failed asserting that 0 matches expected 1.

    /home/sb/EqualsTest.php:6

    2) EqualsTest::testFailure2
    Failed asserting that two strings are equal.
    --- Expected
    +++ Actual
    @@ @@
    -'bar'
    +'baz'

    /home/sb/EqualsTest.php:11

    3) EqualsTest::testFailure3
    Failed asserting that two strings are equal.
    --- Expected
    +++ Actual
    @@ @@
     'foo
    -bar
    +bah
     baz
     '

    /home/sb/EqualsTest.php:16

    FAILURES!
    Tests: 3, Assertions: 3, Failures: 3.

More specialized comparisons are used for specific argument types for ``$expected`` and ``$actual``, see below.

``assertEquals(float $expected, float $actual[, string $message = '', float $delta = 0])``

Reports an error identified by ``$message`` if the absolute difference between two floats ``$expected`` and ``$actual`` is greater than ``$delta``. If the absolute difference between two floats ``$expected`` and ``$actual`` is less than *or equal to* ``$delta``, the assertion will pass.

Please read "`What Every Computer Scientist Should Know About Floating-Point Arithmetic <http://docs.oracle.com/cd/E19957-01/806-3568/ncg_goldberg.html>`_" to understand why ``$delta`` is neccessary.

.. code-block:: php
    :caption: Usage of assertEquals() with floats
    :name: appendixes.assertions.assertEquals.example2

    <?php
    use PHPUnit\Framework\TestCase;

    class EqualsTest extends TestCase
    {
        public function testSuccess()
        {
            $this->assertEquals(1.0, 1.1, '', 0.1);
        }

        public function testFailure()
        {
            $this->assertEquals(1.0, 1.1);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit EqualsTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    .F

    Time: 0 seconds, Memory: 5.75Mb

    There was 1 failure:

    1) EqualsTest::testFailure
    Failed asserting that 1.1 matches expected 1.0.

    /home/sb/EqualsTest.php:11

    FAILURES!
    Tests: 2, Assertions: 2, Failures: 1.

``assertEquals(DOMDocument $expected, DOMDocument $actual[, string $message = ''])``

Reports an error identified by ``$message`` if the uncommented canonical form of the XML documents represented by the two DOMDocument objects ``$expected`` and ``$actual`` are not equal.

.. code-block:: php
    :caption: Usage of assertEquals() with DOMDocument objects
    :name: appendixes.assertions.assertEquals.example3

    <?php
    use PHPUnit\Framework\TestCase;

    class EqualsTest extends TestCase
    {
        public function testFailure()
        {
            $expected = new DOMDocument;
            $expected->loadXML('<foo><bar/></foo>');

            $actual = new DOMDocument;
            $actual->loadXML('<bar><foo/></bar>');

            $this->assertEquals($expected, $actual);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit EqualsTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) EqualsTest::testFailure
    Failed asserting that two DOM documents are equal.
    --- Expected
    +++ Actual
    @@ @@
     <?xml version="1.0"?>
    -<foo>
    -  <bar/>
    -</foo>
    +<bar>
    +  <foo/>
    +</bar>

    /home/sb/EqualsTest.php:12

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

``assertEquals(object $expected, object $actual[, string $message = ''])``

Reports an error identified by ``$message`` if the two objects ``$expected`` and ``$actual`` do not have equal attribute values.

.. code-block:: php
    :caption: Usage of assertEquals() with objects
    :name: appendixes.assertions.assertEquals.example4

    <?php
    use PHPUnit\Framework\TestCase;

    class EqualsTest extends TestCase
    {
        public function testFailure()
        {
            $expected = new stdClass;
            $expected->foo = 'foo';
            $expected->bar = 'bar';

            $actual = new stdClass;
            $actual->foo = 'bar';
            $actual->baz = 'bar';

            $this->assertEquals($expected, $actual);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit EqualsTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.25Mb

    There was 1 failure:

    1) EqualsTest::testFailure
    Failed asserting that two objects are equal.
    --- Expected
    +++ Actual
    @@ @@
     stdClass Object (
    -    'foo' => 'foo'
    -    'bar' => 'bar'
    +    'foo' => 'bar'
    +    'baz' => 'bar'
     )

    /home/sb/EqualsTest.php:14

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

``assertEquals(array $expected, array $actual[, string $message = ''])``

Reports an error identified by ``$message`` if the two arrays ``$expected`` and ``$actual`` are not equal.

.. code-block:: php
    :caption: Usage of assertEquals() with arrays
    :name: appendixes.assertions.assertEquals.example5

    <?php
    use PHPUnit\Framework\TestCase;

    class EqualsTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertEquals(['a', 'b', 'c'], ['a', 'c', 'd']);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit EqualsTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.25Mb

    There was 1 failure:

    1) EqualsTest::testFailure
    Failed asserting that two arrays are equal.
    --- Expected
    +++ Actual
    @@ @@
     Array (
         0 => 'a'
    -    1 => 'b'
    -    2 => 'c'
    +    1 => 'c'
    +    2 => 'd'
     )

    /home/sb/EqualsTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertFalse:

assertFalse()
#############

``assertFalse(bool $condition[, string $message = ''])``

Reports an error identified by ``$message`` if ``$condition`` is ``true``.

``assertNotFalse()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertFalse()
    :name: appendixes.assertions.assertFalse.example

    <?php
    use PHPUnit\Framework\TestCase;

    class FalseTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertFalse(true);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit FalseTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) FalseTest::testFailure
    Failed asserting that true is false.

    /home/sb/FalseTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertFileEquals:

assertFileEquals()
##################

``assertFileEquals(string $expected, string $actual[, string $message = ''])``

Reports an error identified by ``$message`` if the file specified by ``$expected`` does not have the same contents as the file specified by ``$actual``.

``assertFileNotEquals()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertFileEquals()
    :name: appendixes.assertions.assertFileEquals.example

    <?php
    use PHPUnit\Framework\TestCase;

    class FileEqualsTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertFileEquals('/home/sb/expected', '/home/sb/actual');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit FileEqualsTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.25Mb

    There was 1 failure:

    1) FileEqualsTest::testFailure
    Failed asserting that two strings are equal.
    --- Expected
    +++ Actual
    @@ @@
    -'expected
    +'actual
     '

    /home/sb/FileEqualsTest.php:6

    FAILURES!
    Tests: 1, Assertions: 3, Failures: 1.

.. _appendixes.assertions.assertFileExists:

assertFileExists()
##################

``assertFileExists(string $filename[, string $message = ''])``

Reports an error identified by ``$message`` if the file specified by ``$filename`` does not exist.

``assertFileNotExists()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertFileExists()
    :name: appendixes.assertions.assertFileExists.example

    <?php
    use PHPUnit\Framework\TestCase;

    class FileExistsTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertFileExists('/path/to/file');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit FileExistsTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 4.75Mb

    There was 1 failure:

    1) FileExistsTest::testFailure
    Failed asserting that file "/path/to/file" exists.

    /home/sb/FileExistsTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertFileIsReadable:

assertFileIsReadable()
######################

``assertFileIsReadable(string $filename[, string $message = ''])``

Reports an error identified by ``$message`` if the file specified by ``$filename`` is not a file or is not readable.

``assertFileNotIsReadable()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertFileIsReadable()
    :name: appendixes.assertions.assertFileIsReadable.example

    <?php
    use PHPUnit\Framework\TestCase;

    class FileIsReadableTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertFileIsReadable('/path/to/file');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit FileIsReadableTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 4.75Mb

    There was 1 failure:

    1) FileIsReadableTest::testFailure
    Failed asserting that "/path/to/file" is readable.

    /home/sb/FileIsReadableTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertFileIsWritable:

assertFileIsWritable()
######################

``assertFileIsWritable(string $filename[, string $message = ''])``

Reports an error identified by ``$message`` if the file specified by ``$filename`` is not a file or is not writable.

``assertFileNotIsWritable()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertFileIsWritable()
    :name: appendixes.assertions.assertFileIsWritable.example

    <?php
    use PHPUnit\Framework\TestCase;

    class FileIsWritableTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertFileIsWritable('/path/to/file');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit FileIsWritableTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 4.75Mb

    There was 1 failure:

    1) FileIsWritableTest::testFailure
    Failed asserting that "/path/to/file" is writable.

    /home/sb/FileIsWritableTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertGreaterThan:

assertGreaterThan()
###################

``assertGreaterThan(mixed $expected, mixed $actual[, string $message = ''])``

Reports an error identified by ``$message`` if the value of ``$actual`` is not greater than the value of ``$expected``.

``assertAttributeGreaterThan()`` is a convenience wrapper that uses a ``public``, ``protected``, or ``private`` attribute of a class or object as the actual value.

.. code-block:: php
    :caption: Usage of assertGreaterThan()
    :name: appendixes.assertions.assertGreaterThan.example

    <?php
    use PHPUnit\Framework\TestCase;

    class GreaterThanTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertGreaterThan(2, 1);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit GreaterThanTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) GreaterThanTest::testFailure
    Failed asserting that 1 is greater than 2.

    /home/sb/GreaterThanTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertGreaterThanOrEqual:

assertGreaterThanOrEqual()
##########################

``assertGreaterThanOrEqual(mixed $expected, mixed $actual[, string $message = ''])``

Reports an error identified by ``$message`` if the value of ``$actual`` is not greater than or equal to the value of ``$expected``.

``assertAttributeGreaterThanOrEqual()`` is a convenience wrapper that uses a ``public``, ``protected``, or ``private`` attribute of a class or object as the actual value.

.. code-block:: php
    :caption: Usage of assertGreaterThanOrEqual()
    :name: appendixes.assertions.assertGreaterThanOrEqual.example

    <?php
    use PHPUnit\Framework\TestCase;

    class GreatThanOrEqualTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertGreaterThanOrEqual(2, 1);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit GreaterThanOrEqualTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.25Mb

    There was 1 failure:

    1) GreatThanOrEqualTest::testFailure
    Failed asserting that 1 is equal to 2 or is greater than 2.

    /home/sb/GreaterThanOrEqualTest.php:6

    FAILURES!
    Tests: 1, Assertions: 2, Failures: 1.

.. _appendixes.assertions.assertInfinite:

assertInfinite()
################

``assertInfinite(mixed $variable[, string $message = ''])``

Reports an error identified by ``$message`` if ``$variable`` is not ``INF``.

``assertFinite()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertInfinite()
    :name: appendixes.assertions.assertInfinite.example

    <?php
    use PHPUnit\Framework\TestCase;

    class InfiniteTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertInfinite(1);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit InfiniteTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) InfiniteTest::testFailure
    Failed asserting that 1 is infinite.

    /home/sb/InfiniteTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertInstanceOf:

assertInstanceOf()
##################

``assertInstanceOf($expected, $actual[, $message = ''])``

Reports an error identified by ``$message`` if ``$actual`` is not an instance of ``$expected``.

``assertNotInstanceOf()`` is the inverse of this assertion and takes the same arguments.

``assertAttributeInstanceOf()`` and ``assertAttributeNotInstanceOf()`` are convenience wrappers that can be applied to a ``public``, ``protected``, or ``private`` attribute of a class or object.

.. code-block:: php
    :caption: Usage of assertInstanceOf()
    :name: appendixes.assertions.assertInstanceOf.example

    <?php
    use PHPUnit\Framework\TestCase;

    class InstanceOfTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertInstanceOf(RuntimeException::class, new Exception);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit InstanceOfTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) InstanceOfTest::testFailure
    Failed asserting that Exception Object (...) is an instance of class "RuntimeException".

    /home/sb/InstanceOfTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertInternalType:

assertInternalType()
####################

``assertInternalType($expected, $actual[, $message = ''])``

Reports an error identified by ``$message`` if ``$actual`` is not of the ``$expected`` type.

``assertNotInternalType()`` is the inverse of this assertion and takes the same arguments.

``assertAttributeInternalType()`` and ``assertAttributeNotInternalType()`` are convenience wrappers that can be applied to a ``public``, ``protected``, or ``private`` attribute of a class or object.

.. code-block:: php
    :caption: Usage of assertInternalType()
    :name: appendixes.assertions.assertInternalType.example

    <?php
    use PHPUnit\Framework\TestCase;

    class InternalTypeTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertInternalType('string', 42);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit InternalTypeTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) InternalTypeTest::testFailure
    Failed asserting that 42 is of type "string".

    /home/sb/InternalTypeTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertIsReadable:

assertIsReadable()
##################

``assertIsReadable(string $filename[, string $message = ''])``

Reports an error identified by ``$message`` if the file or directory specified by ``$filename`` is not readable.

``assertNotIsReadable()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertIsReadable()
    :name: appendixes.assertions.assertIsReadable.example

    <?php
    use PHPUnit\Framework\TestCase;

    class IsReadableTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertIsReadable('/path/to/unreadable');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit IsReadableTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 4.75Mb

    There was 1 failure:

    1) IsReadableTest::testFailure
    Failed asserting that "/path/to/unreadable" is readable.

    /home/sb/IsReadableTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertIsWritable:

assertIsWritable()
##################

``assertIsWritable(string $filename[, string $message = ''])``

Reports an error identified by ``$message`` if the file or directory specified by ``$filename`` is not writable.

``assertNotIsWritable()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertIsWritable()
    :name: appendixes.assertions.assertIsWritable.example

    <?php
    use PHPUnit\Framework\TestCase;

    class IsWritableTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertIsWritable('/path/to/unwritable');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit IsWritableTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 4.75Mb

    There was 1 failure:

    1) IsWritableTest::testFailure
    Failed asserting that "/path/to/unwritable" is writable.

    /home/sb/IsWritableTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertJsonFileEqualsJsonFile:

assertJsonFileEqualsJsonFile()
##############################

``assertJsonFileEqualsJsonFile(mixed $expectedFile, mixed $actualFile[, string $message = ''])``

Reports an error identified by ``$message`` if the value of ``$actualFile`` does not match the value of
``$expectedFile``.

.. code-block:: php
    :caption: Usage of assertJsonFileEqualsJsonFile()
    :name: appendixes.assertions.assertJsonFileEqualsJsonFile.example

    <?php
    use PHPUnit\Framework\TestCase;

    class JsonFileEqualsJsonFileTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertJsonFileEqualsJsonFile(
              'path/to/fixture/file', 'path/to/actual/file');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit JsonFileEqualsJsonFileTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) JsonFileEqualsJsonFile::testFailure
    Failed asserting that '{"Mascot":"Tux"}' matches JSON string "["Mascott", "Tux", "OS", "Linux"]".

    /home/sb/JsonFileEqualsJsonFileTest.php:5

    FAILURES!
    Tests: 1, Assertions: 3, Failures: 1.

.. _appendixes.assertions.assertJsonStringEqualsJsonFile:

assertJsonStringEqualsJsonFile()
################################

``assertJsonStringEqualsJsonFile(mixed $expectedFile, mixed $actualJson[, string $message = ''])``

Reports an error identified by ``$message`` if the value of ``$actualJson`` does not match the value of
``$expectedFile``.

.. code-block:: php
    :caption: Usage of assertJsonStringEqualsJsonFile()
    :name: appendixes.assertions.assertJsonStringEqualsJsonFile.example

    <?php
    use PHPUnit\Framework\TestCase;

    class JsonStringEqualsJsonFileTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertJsonStringEqualsJsonFile(
                'path/to/fixture/file', json_encode(['Mascot' => 'ux'])
            );
        }
    }
    ?>

.. code-block:: bash

    $ phpunit JsonStringEqualsJsonFileTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) JsonStringEqualsJsonFile::testFailure
    Failed asserting that '{"Mascot":"ux"}' matches JSON string "{"Mascott":"Tux"}".

    /home/sb/JsonStringEqualsJsonFileTest.php:5

    FAILURES!
    Tests: 1, Assertions: 3, Failures: 1.

.. _appendixes.assertions.assertJsonStringEqualsJsonString:

assertJsonStringEqualsJsonString()
##################################

``assertJsonStringEqualsJsonString(mixed $expectedJson, mixed $actualJson[, string $message = ''])``

Reports an error identified by ``$message`` if the value of ``$actualJson`` does not match the value of
``$expectedJson``.

.. code-block:: php
    :caption: Usage of assertJsonStringEqualsJsonString()
    :name: appendixes.assertions.assertJsonStringEqualsJsonString.example

    <?php
    use PHPUnit\Framework\TestCase;

    class JsonStringEqualsJsonStringTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertJsonStringEqualsJsonString(
                json_encode(['Mascot' => 'Tux']),
                json_encode(['Mascot' => 'ux'])
            );
        }
    }
    ?>

.. code-block:: bash

    $ phpunit JsonStringEqualsJsonStringTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) JsonStringEqualsJsonStringTest::testFailure
    Failed asserting that two objects are equal.
    --- Expected
    +++ Actual
    @@ @@
     stdClass Object (
     -    'Mascot' => 'Tux'
     +    'Mascot' => 'ux'
    )

    /home/sb/JsonStringEqualsJsonStringTest.php:5

    FAILURES!
    Tests: 1, Assertions: 3, Failures: 1.

.. _appendixes.assertions.assertLessThan:

assertLessThan()
################

``assertLessThan(mixed $expected, mixed $actual[, string $message = ''])``

Reports an error identified by ``$message`` if the value of ``$actual`` is not less than the value of ``$expected``.

``assertAttributeLessThan()`` is a convenience wrapper that uses a ``public``, ``protected``, or ``private`` attribute of a class or object as the actual value.

.. code-block:: php
    :caption: Usage of assertLessThan()
    :name: appendixes.assertions.assertLessThan.example

    <?php
    use PHPUnit\Framework\TestCase;

    class LessThanTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertLessThan(1, 2);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit LessThanTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) LessThanTest::testFailure
    Failed asserting that 2 is less than 1.

    /home/sb/LessThanTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertLessThanOrEqual:

assertLessThanOrEqual()
#######################

``assertLessThanOrEqual(mixed $expected, mixed $actual[, string $message = ''])``

Reports an error identified by ``$message`` if the value of ``$actual`` is not less than or equal to the value of ``$expected``.

``assertAttributeLessThanOrEqual()`` is a convenience wrapper that uses a ``public``, ``protected``, or ``private`` attribute of a class or object as the actual value.

.. code-block:: php
    :caption: Usage of assertLessThanOrEqual()
    :name: appendixes.assertions.assertLessThanOrEqual.example

    <?php
    use PHPUnit\Framework\TestCase;

    class LessThanOrEqualTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertLessThanOrEqual(1, 2);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit LessThanOrEqualTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.25Mb

    There was 1 failure:

    1) LessThanOrEqualTest::testFailure
    Failed asserting that 2 is equal to 1 or is less than 1.

    /home/sb/LessThanOrEqualTest.php:6

    FAILURES!
    Tests: 1, Assertions: 2, Failures: 1.

.. _appendixes.assertions.assertNan:

assertNan()
###########

``assertNan(mixed $variable[, string $message = ''])``

Reports an error identified by ``$message`` if ``$variable`` is not ``NAN``.

.. code-block:: php
    :caption: Usage of assertNan()
    :name: appendixes.assertions.assertNan.example

    <?php
    use PHPUnit\Framework\TestCase;

    class NanTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertNan(1);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit NanTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) NanTest::testFailure
    Failed asserting that 1 is nan.

    /home/sb/NanTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertNull:

assertNull()
############

``assertNull(mixed $variable[, string $message = ''])``

Reports an error identified by ``$message`` if ``$variable`` is not ``null``.

``assertNotNull()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertNull()
    :name: appendixes.assertions.assertNull.example

    <?php
    use PHPUnit\Framework\TestCase;

    class NullTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertNull('foo');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit NotNullTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) NullTest::testFailure
    Failed asserting that 'foo' is null.

    /home/sb/NotNullTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertObjectHasAttribute:

assertObjectHasAttribute()
##########################

``assertObjectHasAttribute(string $attributeName, object $object[, string $message = ''])``

Reports an error identified by ``$message`` if ``$object->attributeName`` does not exist.

``assertObjectNotHasAttribute()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertObjectHasAttribute()
    :name: appendixes.assertions.assertObjectHasAttribute.example

    <?php
    use PHPUnit\Framework\TestCase;

    class ObjectHasAttributeTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertObjectHasAttribute('foo', new stdClass);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit ObjectHasAttributeTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 4.75Mb

    There was 1 failure:

    1) ObjectHasAttributeTest::testFailure
    Failed asserting that object of class "stdClass" has attribute "foo".

    /home/sb/ObjectHasAttributeTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertRegExp:

assertRegExp()
##############

``assertRegExp(string $pattern, string $string[, string $message = ''])``

Reports an error identified by ``$message`` if ``$string`` does not match the regular expression ``$pattern``.

``assertNotRegExp()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertRegExp()
    :name: appendixes.assertions.assertRegExp.example

    <?php
    use PHPUnit\Framework\TestCase;

    class RegExpTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertRegExp('/foo/', 'bar');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit RegExpTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) RegExpTest::testFailure
    Failed asserting that 'bar' matches PCRE pattern "/foo/".

    /home/sb/RegExpTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertStringMatchesFormat:

assertStringMatchesFormat()
###########################

``assertStringMatchesFormat(string $format, string $string[, string $message = ''])``

Reports an error identified by ``$message`` if the ``$string`` does not match the ``$format`` string.

``assertStringNotMatchesFormat()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertStringMatchesFormat()
    :name: appendixes.assertions.assertStringMatchesFormat.example

    <?php
    use PHPUnit\Framework\TestCase;

    class StringMatchesFormatTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertStringMatchesFormat('%i', 'foo');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit StringMatchesFormatTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) StringMatchesFormatTest::testFailure
    Failed asserting that 'foo' matches PCRE pattern "/^[+-]?\d+$/s".

    /home/sb/StringMatchesFormatTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

The format string may contain the following placeholders:

-

  ``%e``: Represents a directory separator, for example ``/`` on Linux.

-

  ``%s``: One or more of anything (character or white space) except the end of line character.

-

  ``%S``: Zero or more of anything (character or white space) except the end of line character.

-

  ``%a``: One or more of anything (character or white space) including the end of line character.

-

  ``%A``: Zero or more of anything (character or white space) including the end of line character.

-

  ``%w``: Zero or more white space characters.

-

  ``%i``: A signed integer value, for example ``+3142``, ``-3142``.

-

  ``%d``: An unsigned integer value, for example ``123456``.

-

  ``%x``: One or more hexadecimal character. That is, characters in the range ``0-9``, ``a-f``, ``A-F``.

-

  ``%f``: A floating point number, for example: ``3.142``, ``-3.142``, ``3.142E-10``, ``3.142e+10``.

-

  ``%c``: A single character of any sort.

.. _appendixes.assertions.assertStringMatchesFormatFile:

assertStringMatchesFormatFile()
###############################

``assertStringMatchesFormatFile(string $formatFile, string $string[, string $message = ''])``

Reports an error identified by ``$message`` if the ``$string`` does not match the contents of the ``$formatFile``.

``assertStringNotMatchesFormatFile()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertStringMatchesFormatFile()
    :name: appendixes.assertions.assertStringMatchesFormatFile.example

    <?php
    use PHPUnit\Framework\TestCase;

    class StringMatchesFormatFileTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertStringMatchesFormatFile('/path/to/expected.txt', 'foo');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit StringMatchesFormatFileTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) StringMatchesFormatFileTest::testFailure
    Failed asserting that 'foo' matches PCRE pattern "/^[+-]?\d+
    $/s".

    /home/sb/StringMatchesFormatFileTest.php:6

    FAILURES!
    Tests: 1, Assertions: 2, Failures: 1.

.. _appendixes.assertions.assertSame:

assertSame()
############

``assertSame(mixed $expected, mixed $actual[, string $message = ''])``

Reports an error identified by ``$message`` if the two variables ``$expected`` and ``$actual`` do not have the same type and value.

``assertNotSame()`` is the inverse of this assertion and takes the same arguments.

``assertAttributeSame()`` and ``assertAttributeNotSame()`` are convenience wrappers that use a ``public``, ``protected``, or ``private`` attribute of a class or object as the actual value.

.. code-block:: php
    :caption: Usage of assertSame()
    :name: appendixes.assertions.assertSame.example

    <?php
    use PHPUnit\Framework\TestCase;

    class SameTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertSame('2204', 2204);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit SameTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) SameTest::testFailure
    Failed asserting that 2204 is identical to '2204'.

    /home/sb/SameTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

``assertSame(object $expected, object $actual[, string $message = ''])``

Reports an error identified by ``$message`` if the two variables ``$expected`` and ``$actual`` do not reference the same object.

.. code-block:: php
    :caption: Usage of assertSame() with objects
    :name: appendixes.assertions.assertSame.example2

    <?php
    use PHPUnit\Framework\TestCase;

    class SameTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertSame(new stdClass, new stdClass);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit SameTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 4.75Mb

    There was 1 failure:

    1) SameTest::testFailure
    Failed asserting that two variables reference the same object.

    /home/sb/SameTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertStringEndsWith:

assertStringEndsWith()
######################

``assertStringEndsWith(string $suffix, string $string[, string $message = ''])``

Reports an error identified by ``$message`` if the ``$string`` does not end with ``$suffix``.

``assertStringEndsNotWith()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertStringEndsWith()
    :name: appendixes.assertions.assertStringEndsWith.example

    <?php
    use PHPUnit\Framework\TestCase;

    class StringEndsWithTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertStringEndsWith('suffix', 'foo');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit StringEndsWithTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 1 second, Memory: 5.00Mb

    There was 1 failure:

    1) StringEndsWithTest::testFailure
    Failed asserting that 'foo' ends with "suffix".

    /home/sb/StringEndsWithTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertStringEqualsFile:

assertStringEqualsFile()
########################

``assertStringEqualsFile(string $expectedFile, string $actualString[, string $message = ''])``

Reports an error identified by ``$message`` if the file specified by ``$expectedFile`` does not have ``$actualString`` as its contents.

``assertStringNotEqualsFile()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertStringEqualsFile()
    :name: appendixes.assertions.assertStringEqualsFile.example

    <?php
    use PHPUnit\Framework\TestCase;

    class StringEqualsFileTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertStringEqualsFile('/home/sb/expected', 'actual');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit StringEqualsFileTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.25Mb

    There was 1 failure:

    1) StringEqualsFileTest::testFailure
    Failed asserting that two strings are equal.
    --- Expected
    +++ Actual
    @@ @@
    -'expected
    -'
    +'actual'

    /home/sb/StringEqualsFileTest.php:6

    FAILURES!
    Tests: 1, Assertions: 2, Failures: 1.

.. _appendixes.assertions.assertStringStartsWith:

assertStringStartsWith()
########################

``assertStringStartsWith(string $prefix, string $string[, string $message = ''])``

Reports an error identified by ``$message`` if the ``$string`` does not start with ``$prefix``.

``assertStringStartsNotWith()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertStringStartsWith()
    :name: appendixes.assertions.assertStringStartsWith.example

    <?php
    use PHPUnit\Framework\TestCase;

    class StringStartsWithTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertStringStartsWith('prefix', 'foo');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit StringStartsWithTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) StringStartsWithTest::testFailure
    Failed asserting that 'foo' starts with "prefix".

    /home/sb/StringStartsWithTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertThat:

assertThat()
############

More complex assertions can be formulated using the
``PHPUnit\Framework\Constraint`` classes. They can be
evaluated using the ``assertThat()`` method.
:numref:`appendixes.assertions.assertThat.example` shows how the
``logicalNot()`` and ``equalTo()``
constraints can be used to express the same assertion as
``assertNotEquals()``.

``assertThat(mixed $value, PHPUnit\Framework\Constraint $constraint[, $message = ''])``

Reports an error identified by ``$message`` if the ``$value`` does not match the ``$constraint``.

.. code-block:: php
    :caption: Usage of assertThat()
    :name: appendixes.assertions.assertThat.example

    <?php
    use PHPUnit\Framework\TestCase;

    class BiscuitTest extends TestCase
    {
        public function testEquals()
        {
            $theBiscuit = new Biscuit('Ginger');
            $myBiscuit  = new Biscuit('Ginger');

            $this->assertThat(
              $theBiscuit,
              $this->logicalNot(
                $this->equalTo($myBiscuit)
              )
            );
        }
    }
    ?>

:numref:`appendixes.assertions.assertThat.tables.constraints` shows the
available ``PHPUnit\Framework\Constraint`` classes.

.. rst-class:: table
.. list-table:: Constraints
    :name: appendixes.assertions.assertThat.tables.constraints
    :header-rows: 1

    * - Constraint
      - Meaning
    * - ``PHPUnit\Framework\Constraint\Attribute attribute(PHPUnit\Framework\Constraint $constraint, $attributeName)``
      - Constraint that applies another constraint to an attribute of a class or an object.
    * - ``PHPUnit\Framework\Constraint\IsAnything anything()``
      - Constraint that accepts any input value.
    * - ``PHPUnit\Framework\Constraint\ArrayHasKey arrayHasKey(mixed $key)``
      - Constraint that asserts that the array it is evaluated for has a given key.
    * - ``PHPUnit\Framework\Constraint\TraversableContains contains(mixed $value)``
      - Constraint that asserts that the ``array`` or object that implements the ``Iterator`` interface it is evaluated for contains a given value.
    * - ``PHPUnit\Framework\Constraint\TraversableContainsOnly containsOnly(string $type)``
      - Constraint that asserts that the ``array`` or object that implements the ``Iterator`` interface it is evaluated for contains only values of a given type.
    * - ``PHPUnit\Framework\Constraint\TraversableContainsOnly containsOnlyInstancesOf(string $classname)``
      - Constraint that asserts that the ``array`` or object that implements the ``Iterator`` interface it is evaluated for contains only instances of a given classname.
    * - ``PHPUnit\Framework\Constraint\IsEqual equalTo($value, $delta = 0, $maxDepth = 10)``
      - Constraint that checks if one value is equal to another.
    * - ``PHPUnit\Framework\Constraint\Attribute attributeEqualTo($attributeName, $value, $delta = 0, $maxDepth = 10)``
      - Constraint that checks if a value is equal to an attribute of a class or of an object.
    * - ``PHPUnit\Framework\Constraint\DirectoryExists directoryExists()``
      - Constraint that checks if the directory that it is evaluated for exists.
    * - ``PHPUnit\Framework\Constraint\FileExists fileExists()``
      - Constraint that checks if the file(name) that it is evaluated for exists.
    * - ``PHPUnit\Framework\Constraint\IsReadable isReadable()``
      - Constraint that checks if the file(name) that it is evaluated for is readable.
    * - ``PHPUnit\Framework\Constraint\IsWritable isWritable()``
      - Constraint that checks if the file(name) that it is evaluated for is writable.
    * - ``PHPUnit\Framework\Constraint\GreaterThan greaterThan(mixed $value)``
      - Constraint that asserts that the value it is evaluated for is greater than a given value.
    * - ``PHPUnit\Framework\Constraint\Or greaterThanOrEqual(mixed $value)``
      - Constraint that asserts that the value it is evaluated for is greater than or equal to a given value.
    * - ``PHPUnit\Framework\Constraint\ClassHasAttribute classHasAttribute(string $attributeName)``
      - Constraint that asserts that the class it is evaluated for has a given attribute.
    * - ``PHPUnit\Framework\Constraint\ClassHasStaticAttribute classHasStaticAttribute(string $attributeName)``
      - Constraint that asserts that the class it is evaluated for has a given static attribute.
    * - ``PHPUnit\Framework\Constraint\ObjectHasAttribute hasAttribute(string $attributeName)``
      - Constraint that asserts that the object it is evaluated for has a given attribute.
    * - ``PHPUnit\Framework\Constraint\IsIdentical identicalTo(mixed $value)``
      - Constraint that asserts that one value is identical to another.
    * - ``PHPUnit\Framework\Constraint\IsFalse isFalse()``
      - Constraint that asserts that the value it is evaluated is ``false``.
    * - ``PHPUnit\Framework\Constraint\IsInstanceOf isInstanceOf(string $className)``
      - Constraint that asserts that the object it is evaluated for is an instance of a given class.
    * - ``PHPUnit\Framework\Constraint\IsNull isNull()``
      - Constraint that asserts that the value it is evaluated is ``null``.
    * - ``PHPUnit\Framework\Constraint\IsTrue isTrue()``
      - Constraint that asserts that the value it is evaluated is ``true``.
    * - ``PHPUnit\Framework\Constraint\IsType isType(string $type)``
      - Constraint that asserts that the value it is evaluated for is of a specified type.
    * - ``PHPUnit\Framework\Constraint\LessThan lessThan(mixed $value)``
      - Constraint that asserts that the value it is evaluated for is smaller than a given value.
    * - ``PHPUnit\Framework\Constraint\Or lessThanOrEqual(mixed $value)``
      - Constraint that asserts that the value it is evaluated for is smaller than or equal to a given value.
    * - ``logicalAnd()``
      - Logical AND.
    * - ``logicalNot(PHPUnit\Framework\Constraint $constraint)``
      - Logical NOT.
    * - ``logicalOr()``
      - Logical OR.
    * - ``logicalXor()``
      - Logical XOR.
    * - ``PHPUnit\Framework\Constraint\PCREMatch matchesRegularExpression(string $pattern)``
      - Constraint that asserts that the string it is evaluated for matches a regular expression.
    * - ``PHPUnit\Framework\Constraint\StringContains stringContains(string $string, bool $case)``
      - Constraint that asserts that the string it is evaluated for contains a given string.
    * - ``PHPUnit\Framework\Constraint\StringEndsWith stringEndsWith(string $suffix)``
      - Constraint that asserts that the string it is evaluated for ends with a given suffix.
    * - ``PHPUnit\Framework\Constraint\StringStartsWith stringStartsWith(string $prefix)``
      - Constraint that asserts that the string it is evaluated for starts with a given prefix.

.. _appendixes.assertions.assertTrue:

assertTrue()
############

``assertTrue(bool $condition[, string $message = ''])``

Reports an error identified by ``$message`` if ``$condition`` is ``false``.

``assertNotTrue()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertTrue()
    :name: appendixes.assertions.assertTrue.example

    <?php
    use PHPUnit\Framework\TestCase;

    class TrueTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertTrue(false);
        }
    }
    ?>

.. code-block:: bash

    $ phpunit TrueTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) TrueTest::testFailure
    Failed asserting that false is true.

    /home/sb/TrueTest.php:6

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.

.. _appendixes.assertions.assertXmlFileEqualsXmlFile:

assertXmlFileEqualsXmlFile()
############################

``assertXmlFileEqualsXmlFile(string $expectedFile, string $actualFile[, string $message = ''])``

Reports an error identified by ``$message`` if the XML document in ``$actualFile`` is not equal to the XML document in ``$expectedFile``.

``assertXmlFileNotEqualsXmlFile()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertXmlFileEqualsXmlFile()
    :name: appendixes.assertions.assertXmlFileEqualsXmlFile.example

    <?php
    use PHPUnit\Framework\TestCase;

    class XmlFileEqualsXmlFileTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertXmlFileEqualsXmlFile(
              '/home/sb/expected.xml', '/home/sb/actual.xml');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit XmlFileEqualsXmlFileTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.25Mb

    There was 1 failure:

    1) XmlFileEqualsXmlFileTest::testFailure
    Failed asserting that two DOM documents are equal.
    --- Expected
    +++ Actual
    @@ @@
     <?xml version="1.0"?>
     <foo>
    -  <bar/>
    +  <baz/>
     </foo>

    /home/sb/XmlFileEqualsXmlFileTest.php:7

    FAILURES!
    Tests: 1, Assertions: 3, Failures: 1.

.. _appendixes.assertions.assertXmlStringEqualsXmlFile:

assertXmlStringEqualsXmlFile()
##############################

``assertXmlStringEqualsXmlFile(string $expectedFile, string $actualXml[, string $message = ''])``

Reports an error identified by ``$message`` if the XML document in ``$actualXml`` is not equal to the XML document in ``$expectedFile``.

``assertXmlStringNotEqualsXmlFile()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertXmlStringEqualsXmlFile()
    :name: appendixes.assertions.assertXmlStringEqualsXmlFile.example

    <?php
    use PHPUnit\Framework\TestCase;

    class XmlStringEqualsXmlFileTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertXmlStringEqualsXmlFile(
              '/home/sb/expected.xml', '<foo><baz/></foo>');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit XmlStringEqualsXmlFileTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.25Mb

    There was 1 failure:

    1) XmlStringEqualsXmlFileTest::testFailure
    Failed asserting that two DOM documents are equal.
    --- Expected
    +++ Actual
    @@ @@
     <?xml version="1.0"?>
     <foo>
    -  <bar/>
    +  <baz/>
     </foo>

    /home/sb/XmlStringEqualsXmlFileTest.php:7

    FAILURES!
    Tests: 1, Assertions: 2, Failures: 1.

.. _appendixes.assertions.assertXmlStringEqualsXmlString:

assertXmlStringEqualsXmlString()
################################

``assertXmlStringEqualsXmlString(string $expectedXml, string $actualXml[, string $message = ''])``

Reports an error identified by ``$message`` if the XML document in ``$actualXml`` is not equal to the XML document in ``$expectedXml``.

``assertXmlStringNotEqualsXmlString()`` is the inverse of this assertion and takes the same arguments.

.. code-block:: php
    :caption: Usage of assertXmlStringEqualsXmlString()
    :name: appendixes.assertions.assertXmlStringEqualsXmlString.example

    <?php
    use PHPUnit\Framework\TestCase;

    class XmlStringEqualsXmlStringTest extends TestCase
    {
        public function testFailure()
        {
            $this->assertXmlStringEqualsXmlString(
              '<foo><bar/></foo>', '<foo><baz/></foo>');
        }
    }
    ?>

.. code-block:: bash

    $ phpunit XmlStringEqualsXmlStringTest
    PHPUnit 7.0.0 by Sebastian Bergmann and contributors.

    F

    Time: 0 seconds, Memory: 5.00Mb

    There was 1 failure:

    1) XmlStringEqualsXmlStringTest::testFailure
    Failed asserting that two DOM documents are equal.
    --- Expected
    +++ Actual
    @@ @@
     <?xml version="1.0"?>
     <foo>
    -  <bar/>
    +  <baz/>
     </foo>

    /home/sb/XmlStringEqualsXmlStringTest.php:7

    FAILURES!
    Tests: 1, Assertions: 1, Failures: 1.


