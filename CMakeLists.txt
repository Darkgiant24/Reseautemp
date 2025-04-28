cmake_minimum_required(VERSION 3.30)
project(MagnumBootstrap)

# Ajout du chemin des modules
set(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/modules/" ${CMAKE_MODULE_PATH})

# Ajout des sous-dossiers externes
add_subdirectory(externals)

# Recherche des dépendances nécessaires
find_package(Magnum REQUIRED
        GL
        GlfwApplication
        Primitives
        Shaders
        Trade
        MeshTools
        Primitives
        SceneGraph)
find_package(MagnumIntegration REQUIRED ImGui Bullet)
find_package(Bullet REQUIRED Dynamics)

# Configuration des propriétés du projet
set_directory_properties(PROPERTIES CORRADE_USE_PEDANTIC_FLAGS ON)

# Ajout des répertoires d'inclusion
include_directories(${CMAKE_SOURCE_DIR}/externals)

# Définition de l'exécutable principal
add_executable(MagnumBootstrap
        src/main.cpp)

# Ajout des répertoires d'inclusion spécifiques à l'exécutable
target_include_directories(MagnumBootstrap PUBLIC inc)

# Définition de la version de C++ utilisée
set_property(TARGET MagnumBootstrap PROPERTY CXX_STANDARD 20)

# Liaison des bibliothèques nécessaires à l'exécutable
target_link_libraries(MagnumBootstrap PRIVATE
        Magnum::Application
        Magnum::GL
        Magnum::Magnum
        Magnum::MeshTools
        Magnum::Primitives
        Magnum::SceneGraph
        Magnum::Shaders
        Magnum::Trade
        MagnumIntegration::Bullet
        Bullet::Dynamics
        MagnumIntegration::ImGui
        BulletDynamics
        BulletCollision
        LinearMath
        Bullet3Common
        ws2_32 # Add the Winsock library
)