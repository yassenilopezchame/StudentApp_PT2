## PREGUNTAS

## 1. ¿Por qué `onPress={handlePress}` y no `onPress={handlePress()}`?
`onPress` espera una función que se ejecutará cuando ocurra el evento. Si escribimos `handlePress()`, la llama inmediatamente al renderizar y pasa su resultado (normalmente `undefined`). Con `onPress={handlePress}` pasa la referencia a la función, y React Native la invoca al pulsar.

## 2. Diferencia entre `Button` y `Pressable`. ¿Cuándo elegir cada uno?
`Button` se usa para acciones rápidas tipo "compartir" y `Pressable` para botones personalizados de la interfaz.

## 3. ¿Qué recibe la función `style` de `Pressable` y qué devuelve? Ejemplo.
Recibe un objeto con el estado de interacción, como `{ pressed }`, y devuelve los estilos a aplicar (objeto o array). 

## 4. ¿Por qué no se puede cambiar un estado directamente y qué se hace en su lugar?
Porque las variables de `useState` son de solo lectura durante el render. En su lugar se usa el setter, por ejemplo `setIsFollowing(!isFollowing)`, que programa una nueva renderización con el valor actualizado.

## 5. ¿Por qué `followers` no es un segundo `useState`? ¿Qué es un valor derivado?
Porque `followers` se puede calcular a partir de `isFollowing` y `BASE_FOLLOWERS`; guardarlo en otro estado duplicaría la fuente de verdad y podría desincronizarse. Un valor derivado es una variable calculada en el render a partir del estado, como `const followers = BASE_FOLLOWERS + (isFollowing ? 1 : 0)`.

## 6. ¿Qué es una entrada controlada en `TextInput`? ¿Qué dos props la hacen controlada?
Significa que el valor mostrado lo dicta el estado de React, no el componente interno. Las dos props son `value` (lee el estado) y `onChangeText` (actualiza el estado con cada pulsación), de modo que `message` siempre refleja lo que se ve.

## 7. ¿Por qué `selectedSkills.push(skill)` es incorrecto y cuál es el código correcto?
Porque `push` muta el array existente. React compara por referencia y no detecta el cambio, así que no re-renderiza. Lo correcto es crear un array nuevo: `setSelectedSkills(prev => prev.includes(skill) ? prev.filter(s => s !== skill) : [...prev, skill])`.