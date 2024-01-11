Temperature.cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class Temperature : MonoBehaviour
{
public Health health;
public int playerDamage = 2;
public float temperatureCurrent = 36.6f;
public float temperatureNormal = 36.6f;
public float temperatureCritical = 34f;
public float freezeSpeed = 0.05f;
float freezeDamageTimer = 1;
public float freezeDamageDelay = 2;
void Update()
{

temperatureCurrent -= freezeSpeed * Time.deltaTime;

if (temperatureCurrent <= temperatureCritical)
{
if (freezeDamageTimer <= 0)
{
health.TakeDamage(playerDamage);
freezeDamageTimer += freezeDamageDelay;
}
else
 
{
freezeDamageTimer -= Time.deltaTime;
}
}
}
}
Bonfire.cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class Bonfire : MonoBehaviour
{

public float lifeTime = 15;

public float heatPower = 0.1f;

void Update()
{
lifeTime -= Time.deltaTime;
if (lifeTime <= 0)
{
gameObject.SetActive(false);
}
}
void OnTriggerStay(Collider other)
{
if (other.GetComponent<Temperature>() != null)
{
Temperature temperature = other.GetComponent<Temperature>();

if (temperature.temperatureCurrent < temperature.temperatureNormal)
{
temperature.temperatureCurrent += heatPower * Time.deltaTime;
}
}
}
}
TemperatureUI.cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using TMPro;
public class TemperatureUI : MonoBehaviour
{
public Temperature temperature;
public TextMeshProUGUI temperatureText;
void Update()
{
float roundTemperature = Mathf.Round(temperature.temperatureCurrent * 10.0f) * 0.1f;
temperatureText.text = roundTemperature.ToString();

}
}
StartButton.cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;
public class StartButton : MonoBehaviour
{
public void StartGame()
{
SceneManager.LoadScene(1);
}
}
ExitButton.cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;
public class ExitButton : MonoBehaviour
{
public void ExitGame()
{
Application.Quit();
Debug.Log("Мы вышли из игры");
}
}