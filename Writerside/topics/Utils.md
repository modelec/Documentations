# Utils

## Objectif
Fonction utilitaire pour le développement utile pour plusieurs Nodes.

### Variable
PI -> 3.14159265358979323846

### Fonctions
#### `std::vector<std::string> split(const std::string &s, char delim)`
Découpe une chaîne de caractères en fonction d'un délimiteur.

#### `std::string join(const std::vector<std::string> &v, const std::string &delim)`
Joint un vecteur de chaînes de caractères en une seule chaîne, séparée par un délimiteur.

#### `bool startsWith(const std::string &s, const std::string &prefix)`
Vérifie si une chaîne commence par un certain préfixe.

#### `bool endsWith(const std::string &s, const std::string &suffix)`
Vérifie si une chaîne se termine par un certain suffixe.

#### `bool contains(const std::string &s, const std::string &substring)`
Vérifie si une chaîne contient une sous-chaîne.

#### `T mapValue(T v, T v_min, T v_max, T v_min_prime, T v_max_prime)`
Mappe une valeur d'un intervalle à un autre.