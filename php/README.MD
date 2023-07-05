# Astuce php

## long traitemenent

```php
ini_set('max_execution_time', '3600');
ini_set('memory_limit', '1G');
```

## flush en cour de traitement

```php
ob_implicit_flush(true);
```

## Afficher les erreurs

```php
ini_set('display_errors', 1);
ini_set('display_startup_errors', 1);
error_reporting(E_ALL);
```

## Utisation mémoire instantanée

```php
memory_get_usage(true);
```

## Pic max de mémoire

```php
memory_get_peak_usage(true);
```

## Enable garbage collector

```php
gc_enable();
```

## Force garbage collector

```php
gc_collect_cycles();
```
