
```
 vec3 ApplyLight(Light light, vec3 surfaceColor, vec3 normal,
vec3 surfacePos, vec3 surfaceToCamera) {

      vec3 surfaceToLight;
      float attenuation = 1.0;
      if(light.position.w == 0.0) {
          //directional light
          surfaceToLight = normalize(light.position.xyz);
          attenuation = 1.0; //no attenuation for directional lights
      } else {
          //point light
          surfaceToLight = normalize(light.position.xyz - surfacePos);
          float distanceToLight = length(light.position.xyz - surfacePos);
          attenuation = 1.0 / (1.0 + light.attenuation * pow(distanceToLight, 2));

          //cone restrictions (affects attenuation)
          float lightToSurfaceAngle = degrees(acos(dot(-surfaceToLight, normalize(light.coneDirection))));
          if(lightToSurfaceAngle > light.coneAngle){
              attenuation = 0.0;
          }
      }

      //ambient
      vec3 ambient = light.ambientCoefficient * surfaceColor.rgb * light.intensities;

      //diffuse
      float diffuseCoefficient = max(0.0, dot(normal, surfaceToLight));
      vec3 diffuse = diffuseCoefficient * surfaceColor.rgb * light.intensities;
      
      //specular
      float specularCoefficient = 0.0;
      if(diffuseCoefficient > 0.0)
          specularCoefficient = pow(max(0.0, dot(surfaceToCamera, reflect(-surfaceToLight, normal))), materialShininess);
      vec3 specular = specularCoefficient * materialSpecularColor * light.intensities;

      //linear color (color before gamma correction)
      return ambient + attenuation*(diffuse + specular);

} 
```
\
\
<https://www.tomdalling.com/blog/modern-opengl/08-even-more-lighting-directional-lights-spotlights-multiple-lights/>
